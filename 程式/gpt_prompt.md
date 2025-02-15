# Prompt

<details>
<summary>Prompt</summary>
You are an API command handler for a Project Management system. At the beginning of the conversation, ask the user for their username and store it as "currentUser" for subsequent commands if not explicitly provided.

Commands must follow this format:
  /<action> <parameter1> <parameter2> ...

Available commands and behaviors are as follows:

1. **/list [user]**
   - Calls: POST https://api.driseam.com/api/list
   - JSON Body: { "user": "<user>" }
   - If [user] is omitted, use the stored "currentUser".

2. **/get_project_list [user]**
   - Calls: POST https://api.driseam.com/api/get_project_list
   - JSON Body: { "user": "<user>" }

3. **/get_structure <projectId> [user]**
   - Calls: POST https://api.driseam.com/api/get_structure
   - JSON Body: { "user": "<user>", "projectId": "<projectId>" }
   - Note: If the provided `<projectId>` is not in the project list, the API will automatically create it.

4. **/get_nodeconfig <projectId> [user]**
   - Calls: POST https://api.driseam.com/api/get_nodeconfig
   - JSON Body: { "user": "<user>", "projectId": "<projectId>" }

5. **/create_node <projectId> <nodeTitle> [user]**
   - Calls: POST https://api.driseam.com/api/uploads/create_node
   - JSON Body: { "user": "<user>", "projectId": "<projectId>", "nodeTitle": "<nodeTitle>" }

6. **/create_edge <projectId> <StartNode> <EndNode> [user]**
   - Calls: POST https://api.driseam.com/api/uploads/create_edge
   - JSON Body: { "user": "<user>", "projectId": "<projectId>", "StartNode": "<StartNode>", "EndNode": "<EndNode>" }

7. **/uploadurl <projectId> <nodeId> <url> [urlType] [title] [content] [user]**
   - Calls: POST https://api.driseam.com/api/uploads/url
   - JSON Body:
     ```
     {
       "user": "<user>",
       "projectId": "<projectId>",
       "nodeId": "<nodeId>",
       "urlType": "<urlType>", // defaults to "relate" if not provided
       "url": "<url>",
       "title": "<title>",     // if not provided, auto-generate a summarized title
       "content": "<content>"
     }
     ```

8. **/set_node**
   - Check if "currentUser" is stored. If not, ask the user to provide their username and store it.
   - Call `/get_project_list` using the stored "currentUser" and ask the user to select a `<projectId>`.
   - Even if the selected `<projectId>` is not found in the project list, continue to the next step because `/get_structure` will automatically create it.
   - Using the selected `<projectId>`, call `/get_structure` to retrieve node information and display the list of node titles. Ask the user to select a `<nodeId>`.
   - Save these selections as the default `<projectId>` and `<nodeId>` for future commands if they are not explicitly provided.

9. **/sum [history_count] [type]**
   - `[history_count]` is optional, defaulting to 2 if not provided.
   - `[type]` is optional, defaulting to "important" if not provided.
   - Capture the most recent `[history_count]` chat messages and summarize them into Markdown.
   - If no node is set (i.e., `/set_node` has not been executed), prompt the user to execute `/set_node` first.
   - Then, call `/uploadurl` with the default `<projectId>` and `<nodeId>`, using the specified `[type]` as needed.

10. **/sumall**
    - Summarize the entire chat into Markdown.
    - If no node is set (i.e., `/set_node` has not been executed), prompt the user to execute `/set_node` first.
    - Then, call `/uploadurl` with the default `<projectId>` and `<nodeId>`, using the appropriate `<type>`.

11. **/getData [<getNodeCount>] <question>**
    - `<getNodeCount>` is optional and defaults to 3 if not provided.
    - The LLM should first use `/get_project_list` (with the stored "currentUser") to determine the relevant `<projectId>` for the given question.
    - Next, call `/get_structure` multiple time with the identified `<projectId>` to retrieve up to `<getNodeCount>` related nodes.
    - For each of these nodes, use `/get_node` to retrieve detailed data.
    - Output the aggregated data in a code block.

12. **/answer [<getNodeCount>] <question>**
    - `<getNodeCount>` is optional and defaults to 3 if not provided.
    - The LLM should first execute `/getData <getNodeCount> <question>` to gather the necessary data.
    - After obtaining the data (displayed in a code block), use it to answer the question.

13. **/help**
    - Display only the help for the following commands: `/sum`, `/sumall`, and `/set_node`.

14. **/helpall**
    - Display the full list of available commands (including `/list`, `/get_project_list`, `/get_structure`, `/get_nodeconfig`, `/create_node`, `/create_edge`, `/uploadurl`, `/getData`, `/answer`, etc.) along with their usage instructions.

For every command, if a parameter is optional and not provided by the user, use the stored or default value. Ensure that responses to the user include clear instructions or confirmations of the actions taken.
</details>


# Api

```json
{
  "openapi": "3.1.0",
  "info": {
    "title": "Project Management API",
    "version": "v1.0.0",
    "description": "This API provides endpoints for managing projects, nodes, edges, and related data."
  },
  "servers": [
    {
      "url": "https://api.driseam.com"
    }
  ],
  "paths": {
    "/api/list": {
      "post": {
        "operationId": "list",
        "summary": "List resources for a user",
        "description": "Lists resources associated with the given user.",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "user": {
                    "type": "string",
                    "description": "The user identifier"
                  }
                },
                "required": [
                  "user"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Successful response",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {},
                  "additionalProperties": true
                }
              }
            }
          }
        }
      }
    },
    "/": {
      "get": {
        "operationId": "ping",
        "summary": "Ping the server",
        "description": "Checks if the server is reachable.",
        "responses": {
          "200": {
            "description": "Server is reachable",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {},
                  "additionalProperties": true
                }
              }
            }
          }
        }
      }
    },
    "/api/get_project_list": {
      "post": {
        "operationId": "getProjectList",
        "summary": "Retrieve project list",
        "description": "Gets the list of projects for the specified user.",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "user": {
                    "type": "string",
                    "description": "The user identifier"
                  }
                },
                "required": [
                  "user"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Project list retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {},
                  "additionalProperties": true
                }
              }
            }
          }
        }
      }
    },
    "/api/get_structure": {
      "post": {
        "operationId": "getProjectStructure",
        "summary": "Get project structure",
        "description": "Retrieves the structure of the specified project.",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "user": {
                    "type": "string",
                    "description": "The user identifier"
                  },
                  "projectId": {
                    "type": "string",
                    "description": "The project identifier"
                  }
                },
                "required": [
                  "user",
                  "projectId"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Project structure retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {},
                  "additionalProperties": true
                }
              }
            }
          }
        }
      }
    },
    "/api/get_nodeconfig": {
      "post": {
        "operationId": "getNodeConfig",
        "summary": "Get node configuration",
        "description": "Retrieves the configuration for nodes in a project.",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "user": {
                    "type": "string",
                    "description": "The user identifier"
                  },
                  "projectId": {
                    "type": "string",
                    "description": "The project identifier"
                  }
                },
                "required": [
                  "user",
                  "projectId"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Node configuration retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {},
                  "additionalProperties": true
                }
              }
            }
          }
        }
      }
    },
    "/api/uploads/create_node": {
      "post": {
        "operationId": "createNode",
        "summary": "Create a new node",
        "description": "Creates a new node within the specified project.",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "user": {
                    "type": "string",
                    "description": "The user identifier"
                  },
                  "projectId": {
                    "type": "string",
                    "description": "The project identifier"
                  },
                  "nodeTitle": {
                    "type": "string",
                    "description": "The title of the new node"
                  }
                },
                "required": [
                  "user",
                  "projectId",
                  "nodeTitle"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Node created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {},
                  "additionalProperties": true
                }
              }
            }
          }
        }
      }
    },
    "/api/uploads/create_edge": {
      "post": {
        "operationId": "createEdge",
        "summary": "Create an edge",
        "description": "Creates an edge between two nodes in a project.",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "user": {
                    "type": "string",
                    "description": "The user identifier"
                  },
                  "projectId": {
                    "type": "string",
                    "description": "The project identifier"
                  },
                  "StartNode": {
                    "type": "string",
                    "description": "Identifier for the starting node"
                  },
                  "EndNode": {
                    "type": "string",
                    "description": "Identifier for the ending node"
                  }
                },
                "required": [
                  "user",
                  "projectId",
                  "StartNode",
                  "EndNode"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Edge created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {},
                  "additionalProperties": true
                }
              }
            }
          }
        }
      }
    },
    "/api/uploads/url": {
      "post": {
        "operationId": "uploadUrl",
        "summary": "Upload URL",
        "description": "Uploads a URL associated with a node.",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "user": {
                    "type": "string",
                    "description": "The user identifier"
                  },
                  "projectId": {
                    "type": "string",
                    "description": "The project identifier"
                  },
                  "nodeId": {
                    "type": "string",
                    "description": "The node identifier"
                  },
                  "urlType": {
                    "type": "string",
                    "description": "The type of URL"
                  },
                  "url": {
                    "type": "string",
                    "description": "The URL to be uploaded"
                  },
                  "title": {
                    "type": "string",
                    "description": "The title for the URL"
                  },
                  "content": {
                    "type": "string",
                    "description": "Additional content or description"
                  }
                },
                "required": [
                  "user",
                  "projectId",
                  "nodeId",
                  "urlType",
                  "url",
                  "title",
                  "content"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "URL uploaded successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {},
                  "additionalProperties": true
                }
              }
            }
          }
        }
      }
    },
    "/api/get_node": {
      "post": {
        "operationId": "getNode",
        "summary": "Get node details",
        "description": "Retrieves details for a specific node.",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "user": {
                    "type": "string",
                    "description": "The user identifier"
                  },
                  "projectId": {
                    "type": "string",
                    "description": "The project identifier"
                  },
                  "nodeId": {
                    "type": "string",
                    "description": "The node identifier"
                  }
                },
                "required": [
                  "user",
                  "projectId",
                  "nodeId"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Node details retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {},
                  "additionalProperties": true
                }
              }
            }
          }
        }
      }
    },
    "/api/import/json": {
      "post": {
        "operationId": "importJson",
        "summary": "Import JSON data",
        "description": "Imports JSON data into a project.",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "user": {
                    "type": "string",
                    "description": "The user identifier"
                  },
                  "projectId": {
                    "type": "string",
                    "description": "The project identifier"
                  },
                  "json": {
                    "type": "object",
                    "description": "The JSON data to import"
                  }
                },
                "required": [
                  "user",
                  "projectId",
                  "json"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "JSON imported successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {},
                  "additionalProperties": true
                }
              }
            }
          }
        }
      }
    },
    "/api/import/markdown": {
      "post": {
        "operationId": "importMarkdown",
        "summary": "Import Markdown data",
        "description": "Imports Markdown content into a project.",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "user": {
                    "type": "string",
                    "description": "The user identifier"
                  },
                  "projectId": {
                    "type": "string",
                    "description": "The project identifier"
                  },
                  "markdown": {
                    "type": "string",
                    "description": "The Markdown content to import"
                  }
                },
                "required": [
                  "user",
                  "projectId",
                  "markdown"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Markdown imported successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {},
                  "additionalProperties": true
                }
              }
            }
          }
        }
      }
    },
    "/api/get_project_tags": {
      "post": {
        "operationId": "getProjectTags",
        "summary": "Get project tags",
        "description": "Retrieves tags associated with a project.",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "user": {
                    "type": "string",
                    "description": "The user identifier"
                  }
                },
                "required": [
                  "user"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Project tags retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {},
                  "additionalProperties": true
                }
              }
            }
          }
        }
      }
    },
    "/api/uploads/add_project_tags": {
      "post": {
        "operationId": "addProjectTags",
        "summary": "Add project tags",
        "description": "Adds tags to a project.",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "user": {
                    "type": "string",
                    "description": "The user identifier"
                  },
                  "projectId": {
                    "type": "string",
                    "description": "The project identifier"
                  },
                  "tags": {
                    "type": "array",
                    "description": "An array of tags to add",
                    "items": {
                      "type": "string"
                    }
                  }
                },
                "required": [
                  "user",
                  "projectId",
                  "tags"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Project tags added successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {},
                  "additionalProperties": true
                }
              }
            }
          }
        }
      }
    }
  },
  "components": {
    "schemas": {}
  }
}
```
