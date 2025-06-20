# GitHub MCP Server

The GitHub MCP Server is a [Model Context Protocol (MCP)](https://modelcontextprotocol.io/introduction)
server that provides seamless integration with GitHub APIs, enabling advanced
automation and interaction capabilities for developers and tools.

### Use Cases

- Automating GitHub workflows and processes.
- Extracting and analyzing data from GitHub repositories.
- Building AI powered tools and applications that interact with GitHub's ecosystem.

---

## Remote GitHub MCP Server

[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Server-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=github&config=%7B%22type%22%3A%20%22http%22%2C%22url%22%3A%20%22https%3A%2F%2Fapi.githubcopilot.com%2Fmcp%2F%22%7D) [![Install in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Install_Server-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=github&config=%7B%22type%22%3A%20%22http%22%2C%22url%22%3A%20%22https%3A%2F%2Fapi.githubcopilot.com%2Fmcp%2F%22%7D&quality=insiders)

The remote GitHub MCP Server is hosted by GitHub and provides the easiest method for getting up and running. If your MCP host does not support remote MCP servers, don't worry! You can use the [local version of the GitHub MCP Server](https://github.com/github/github-mcp-server?tab=readme-ov-file#local-github-mcp-server) instead.

## Prerequisites

1. An MCP host that supports the latest MCP specification and remote servers, such as [VS Code](https://code.visualstudio.com/).

## Installation

### Usage with VS Code

For quick installation, use one of the one-click install buttons above. Once you complete that flow, toggle Agent mode (located by the Copilot Chat text input) and the server will start. Make sure you're using [VS Code 1.101](https://code.visualstudio.com/updates/v1_101) or [later](https://code.visualstudio.com/updates) for remote MCP and OAuth support.


Alternatively, to manually configure VS Code, choose the appropriate JSON block from the examples below and add it to your host configuration:

<table>
<tr><th>Using OAuth</th><th>Using a GitHub PAT</th></tr>
<tr><th align=left colspan=2>VS Code (version 1.101 or greater)</th></tr>
<tr valign=top>
<td>
  
```json
{
  "servers": {
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp/"
    }
  }
}
```

</td>
<td>

```json
{
  "servers": {
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp/",
      "headers": {
        "Authorization": "Bearer ${input:github_mcp_pat}"
      }
    }
  },
  "inputs": [
    {
      "type": "promptString",
      "id": "github_mcp_pat",
      "description": "GitHub Personal Access Token",
      "password": true
    }
  ]
}
```

</td>
</tr>
</table>

### Usage in other MCP Hosts

For MCP Hosts that are [Remote MCP-compatible](docs/host-integration.md), choose the appropriate JSON block from the examples below and add it to your host configuration:

<table>
<tr><th>Using OAuth</th><th>Using a GitHub PAT</th></tr>
<tr valign=top>
<td>
  
```json
{
  "mcpServers": {
    "github": {
      "url": "https://api.githubcopilot.com/mcp/"
    }
  }
}
```

</td>
<td>

```json
{
  "mcpServers": {
    "github": {
      "url": "https://api.githubcopilot.com/mcp/",
      "authorization_token": "Bearer <your GitHub PAT>"
    }
  }
}
```

</td>
</tr>
</table>

> **Note:** The exact configuration format may vary by host. Refer to your host's documentation for the correct syntax and location for remote MCP server setup.

### Configuration

See [Remote Server Documentation](docs/remote-server.md) on how to pass additional configuration settings to the remote GitHub MCP Server.

---

## Local GitHub MCP Server

[![Install with Docker in VS Code](https://img.shields.io/badge/VS_Code-Install_Server-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=github&inputs=%5B%7B%22id%22%3A%22github_token%22%2C%22type%22%3A%22promptString%22%2C%22description%22%3A%22GitHub%20Personal%20Access%20Token%22%2C%22password%22%3Atrue%7D%5D&config=%7B%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22-i%22%2C%22--rm%22%2C%22-e%22%2C%22GITHUB_PERSONAL_ACCESS_TOKEN%22%2C%22ghcr.io%2Fgithub%2Fgithub-mcp-server%22%5D%2C%22env%22%3A%7B%22GITHUB_PERSONAL_ACCESS_TOKEN%22%3A%22%24%7Binput%3Agithub_token%7D%22%7D%7D) [![Install with Docker in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Install_Server-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=github&inputs=%5B%7B%22id%22%3A%22github_token%22%2C%22type%22%3A%22promptString%22%2C%22description%22%3A%22GitHub%20Personal%20Access%20Token%22%2C%22password%22%3Atrue%7D%5D&config=%7B%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22-i%22%2C%22--rm%22%2C%22-e%22%2C%22GITHUB_PERSONAL_ACCESS_TOKEN%22%2C%22ghcr.io%2Fgithub%2Fgithub-mcp-server%22%5D%2C%22env%22%3A%7B%22GITHUB_PERSONAL_ACCESS_TOKEN%22%3A%22%24%7Binput%3Agithub_token%7D%22%7D%7D&quality=insiders)

## Prerequisites

1. To run the server in a container, you will need to have [Docker](https://www.docker.com/) installed.
2. Once Docker is installed, you will also need to ensure Docker is running. The image is public; if you get errors on pull, you may have an expired token and need to `docker logout ghcr.io`.
3. Lastly you will need to [Create a GitHub Personal Access Token](https://github.com/settings/personal-access-tokens/new).
The MCP server can use many of the GitHub APIs, so enable the permissions that you feel comfortable granting your AI tools (to learn more about access tokens, please check out the [documentation](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)).

## Installation

### Usage with VS Code

For quick installation, use one of the one-click install buttons. Once you complete that flow, toggle Agent mode (located by the Copilot Chat text input) and the server will start.

### Usage in other MCP Hosts

Add the following JSON block to your IDE MCP settings.

```json
{
  "mcp": {
    "inputs": [
      {
        "type": "promptString",
        "id": "github_token",
        "description": "GitHub Personal Access Token",
        "password": true
      }
    ],
    "servers": {
      "github": {
        "command": "docker",
        "args": [
          "run",
          "-i",
          "--rm",
          "-e",
          "GITHUB_PERSONAL_ACCESS_TOKEN",
          "ghcr.io/github/github-mcp-server"
        ],
        "env": {
          "GITHUB_PERSONAL_ACCESS_TOKEN": "${input:github_token}"
        }
      }
    }
  }
}
```

Optionally, you can add a similar example (i.e. without the mcp key) to a file called `.vscode/mcp.json` in your workspace. This will allow you to share the configuration with others.


```json
{
  "inputs": [
    {
      "type": "promptString",
      "id": "github_token",
      "description": "GitHub Personal Access Token",
      "password": true
    }
  ],
  "servers": {
    "github": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e",
        "GITHUB_PERSONAL_ACCESS_TOKEN",
        "ghcr.io/github/github-mcp-server"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${input:github_token}"
      }
    }
  }
}

```

More about using MCP server tools in VS Code's [agent mode documentation](https://code.visualstudio.com/docs/copilot/chat/mcp-servers).

### Usage with Claude Desktop

```json
{
  "mcpServers": {
    "github": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e",
        "GITHUB_PERSONAL_ACCESS_TOKEN",
        "ghcr.io/github/github-mcp-server"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<YOUR_TOKEN>"
      }
    }
  }
}
```

### Build from source

If you don't have Docker, you can use `go build` to build the binary in the
`cmd/github-mcp-server` directory, and use the `github-mcp-server stdio` command with the `GITHUB_PERSONAL_ACCESS_TOKEN` environment variable set to your token. To specify the output location of the build, use the `-o` flag. You should configure your server to use the built executable as its `command`. For example:

```JSON
{
  "mcp": {
    "servers": {
      "github": {
        "command": "/path/to/github-mcp-server",
        "args": ["stdio"],
        "env": {
          "GITHUB_PERSONAL_ACCESS_TOKEN": "<YOUR_TOKEN>"
        }
      }
    }
  }
}
```

## Tool Configuration

The GitHub MCP Server supports enabling or disabling specific groups of functionalities via the `--toolsets` flag. This allows you to control which GitHub API capabilities are available to your AI tools. Enabling only the toolsets that you need can help the LLM with tool choice and reduce the context size.

_Toolsets are not limited to Tools. Relevant MCP Resources and Prompts are also included where applicable._

### Available Toolsets

The following sets of tools are available (all are on by default):

| Toolset                 | Description                                                   |
| ----------------------- | ------------------------------------------------------------- |
| `actions`               | GitHub Actions workflows and CI/CD operations                |
| `context`               | **Strongly recommended**: Tools that provide context about the current user and GitHub context you are operating in |
| `code_security`         | Code scanning alerts and security features                    |
| `issues`                | Issue-related tools (create, read, update, comment)           |
| `notifications`         | GitHub Notifications related tools                            |
| `pull_requests`         | Pull request operations (create, merge, review)               |
| `projects`              | Manage GitHub Projects V2                                      |
| `repos`                 | Repository-related tools (file operations, branches, commits) |
| `secret_protection`     | Secret protection related tools, such as GitHub Secret Scanning |
| `users`                 | Anything relating to GitHub Users                             |
| `experiments`           | Experimental features (not considered stable)                 |


#### Specifying Toolsets

To specify toolsets you want available to the LLM, you can pass an allow-list in two ways:

1. **Using Command Line Argument**:

   ```bash
   github-mcp-server --toolsets repos,issues,pull_requests,actions,code_security
   ```

2. **Using Environment Variable**:
   ```bash
   GITHUB_TOOLSETS="repos,issues,pull_requests,actions,code_security" ./github-mcp-server
   ```

The environment variable `GITHUB_TOOLSETS` takes precedence over the command line argument if both are provided.

### Using Toolsets With Docker

When using Docker, you can pass the toolsets as environment variables:

```bash
docker run -i --rm \
  -e GITHUB_PERSONAL_ACCESS_TOKEN=<your-token> \
  -e GITHUB_TOOLSETS="repos,issues,pull_requests,actions,code_security,experiments" \
  ghcr.io/github/github-mcp-server
```

### The "all" Toolset

The special toolset `all` can be provided to enable all available toolsets regardless of any other configuration:

```bash
./github-mcp-server --toolsets all
```

Or using the environment variable:

```bash
GITHUB_TOOLSETS="all" ./github-mcp-server
```

## Dynamic Tool Discovery

**Note**: This feature is currently in beta and may not be available in all environments. Please test it out and let us know if you encounter any issues.

Instead of starting with all tools enabled, you can turn on dynamic toolset discovery. Dynamic toolsets allow the MCP host to list and enable toolsets in response to a user prompt. This should help to avoid situations where the model gets confused by the sheer number of tools available.

### Using Dynamic Tool Discovery

When using the binary, you can pass the `--dynamic-toolsets` flag.

```bash
./github-mcp-server --dynamic-toolsets
```

When using Docker, you can pass the toolsets as environment variables:

```bash
docker run -i --rm \
  -e GITHUB_PERSONAL_ACCESS_TOKEN=<your-token> \
  -e GITHUB_DYNAMIC_TOOLSETS=1 \
  ghcr.io/github/github-mcp-server
```

## Read-Only Mode

To run the server in read-only mode, you can use the `--read-only` flag. This will only offer read-only tools, preventing any modifications to repositories, issues, pull requests, etc.

```bash
./github-mcp-server --read-only
```

When using Docker, you can pass the read-only mode as an environment variable:

```bash
docker run -i --rm \
  -e GITHUB_PERSONAL_ACCESS_TOKEN=<your-token> \
  -e GITHUB_READ_ONLY=1 \
  ghcr.io/github/github-mcp-server
```

## GitHub Enterprise Server and Enterprise Cloud with data residency (ghe.com)

The flag `--gh-host` and the environment variable `GITHUB_HOST` can be used to set
the hostname for GitHub Enterprise Server or GitHub Enterprise Cloud with data residency.

- For GitHub Enterprise Server, prefix the hostname with the `https://` URI scheme, as it otherwise defaults to `http://`, which GitHub Enterprise Server does not support.
- For GitHub Enterprise Cloud with data residency, use `https://YOURSUBDOMAIN.ghe.com` as the hostname.
``` json
"github": {
    "command": "docker",
    "args": [
    "run",
    "-i",
    "--rm",
    "-e",
    "GITHUB_PERSONAL_ACCESS_TOKEN",
    "-e",
    "GITHUB_HOST",
    "ghcr.io/github/github-mcp-server"
    ],
    "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${input:github_token}",
        "GITHUB_HOST": "https://<your GHES or ghe.com domain name>"
    }
}
```

## i18n / Overriding Descriptions

The descriptions of the tools can be overridden by creating a
`github-mcp-server-config.json` file in the same directory as the binary.

The file should contain a JSON object with the tool names as keys and the new
descriptions as values. For example:

```json
{
  "TOOL_ADD_ISSUE_COMMENT_DESCRIPTION": "an alternative description",
  "TOOL_CREATE_BRANCH_DESCRIPTION": "Create a new branch in a GitHub repository"
}
```

You can create an export of the current translations by running the binary with
the `--export-translations` flag.

This flag will preserve any translations/overrides you have made, while adding
any new translations that have been added to the binary since the last time you
exported.

```sh
./github-mcp-server --export-translations
cat github-mcp-server-config.json
```

You can also use ENV vars to override the descriptions. The environment
variable names are the same as the keys in the JSON file, prefixed with
`GITHUB_MCP_` and all uppercase.

For example, to override the `TOOL_ADD_ISSUE_COMMENT_DESCRIPTION` tool, you can
set the following environment variable:

```sh
export GITHUB_MCP_TOOL_ADD_ISSUE_COMMENT_DESCRIPTION="an alternative description"
```

## Tools

### Users

- **get_me** - Get details of the authenticated user
  - No parameters required

### Issues

- **get_issue** - Gets the contents of an issue within a repository

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `issue_number`: Issue number (number, required)

- **get_issue_comments** - Get comments for a GitHub issue

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `issue_number`: Issue number (number, required)

- **create_issue** - Create a new issue in a GitHub repository

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `title`: Issue title (string, required)
  - `body`: Issue body content (string, optional)
  - `assignees`: Usernames to assign to this issue (string[], optional)
  - `labels`: Labels to apply to this issue (string[], optional)

- **add_issue_comment** - Add a comment to an issue

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `issue_number`: Issue number (number, required)
  - `body`: Comment text (string, required)

- **list_issues** - List and filter repository issues

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `state`: Filter by state ('open', 'closed', 'all') (string, optional)
  - `labels`: Labels to filter by (string[], optional)
  - `sort`: Sort by ('created', 'updated', 'comments') (string, optional)
  - `direction`: Sort direction ('asc', 'desc') (string, optional)
  - `since`: Filter by date (ISO 8601 timestamp) (string, optional)
  - `page`: Page number (number, optional)
  - `perPage`: Results per page (number, optional)

- **update_issue** - Update an existing issue in a GitHub repository

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `issue_number`: Issue number to update (number, required)
  - `title`: New title (string, optional)
  - `body`: New description (string, optional)
  - `state`: New state ('open' or 'closed') (string, optional)
  - `labels`: New labels (string[], optional)
  - `assignees`: New assignees (string[], optional)
  - `milestone`: New milestone number (number, optional)

- **search_issues** - Search for issues and pull requests
  - `query`: Search query (string, required)
  - `sort`: Sort field (string, optional)
  - `order`: Sort order (string, optional)
  - `page`: Page number (number, optional)
  - `perPage`: Results per page (number, optional)

- **assign_copilot_to_issue** - Assign Copilot to a specific issue in a GitHub repository

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `issueNumber`: Issue number (number, required)
  - _Note_: This tool can help with creating a Pull Request with source code changes to resolve the issue. More information can be found at [GitHub Copilot documentation](https://docs.github.com/en/copilot/using-github-copilot/using-copilot-coding-agent-to-work-on-tasks/about-assigning-tasks-to-copilot)


### Pull Requests

- **get_pull_request** - Get details of a specific pull request

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `pullNumber`: Pull request number (number, required)

- **list_pull_requests** - List and filter repository pull requests

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `state`: PR state (string, optional)
  - `sort`: Sort field (string, optional)
  - `direction`: Sort direction (string, optional)
  - `perPage`: Results per page (number, optional)
  - `page`: Page number (number, optional)

- **merge_pull_request** - Merge a pull request

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `pullNumber`: Pull request number (number, required)
  - `commit_title`: Title for the merge commit (string, optional)
  - `commit_message`: Message for the merge commit (string, optional)
  - `merge_method`: Merge method (string, optional)

- **get_pull_request_files** - Get the list of files changed in a pull request

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `pullNumber`: Pull request number (number, required)

- **get_pull_request_status** - Get the combined status of all status checks for a pull request

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `pullNumber`: Pull request number (number, required)

- **update_pull_request_branch** - Update a pull request branch with the latest changes from the base branch

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `pullNumber`: Pull request number (number, required)
  - `expectedHeadSha`: The expected SHA of the pull request's HEAD ref (string, optional)

- **get_pull_request_comments** - Get the review comments on a pull request

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `pullNumber`: Pull request number (number, required)

- **get_pull_request_reviews** - Get the reviews on a pull request

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `pullNumber`: Pull request number (number, required)

- **get_pull_request_diff** - Get the diff of a pull request

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `pullNumber`: Pull request number (number, required)

- **create_pending_pull_request_review** - Create a pending review for a pull request that can be submitted later

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `pullNumber`: Pull request number (number, required)
  - `commitID`: SHA of commit to review (string, optional)

- **add_pull_request_review_comment_to_pending_review** - Add a comment to the requester's latest pending pull request review

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `pullNumber`: Pull request number (number, required)
  - `path`: The relative path to the file that necessitates a comment (string, required)
  - `body`: The text of the review comment (string, required)
  - `subjectType`: The level at which the comment is targeted (string, required)
    - Enum: "FILE", "LINE"
  - `line`: The line of the blob in the pull request diff that the comment applies to (number, optional)
  - `side`: The side of the diff to comment on (string, optional)
    - Enum: "LEFT", "RIGHT"
  - `startLine`: For multi-line comments, the first line of the range (number, optional)
  - `startSide`: For multi-line comments, the starting side of the diff (string, optional)
    - Enum: "LEFT", "RIGHT"

- **submit_pending_pull_request_review** - Submit the requester's latest pending pull request review

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `pullNumber`: Pull request number (number, required)
  - `event`: The event to perform (string, required)
    - Enum: "APPROVE", "REQUEST_CHANGES", "COMMENT"
  - `body`: The text of the review comment (string, optional)

- **delete_pending_pull_request_review** - Delete the requester's latest pending pull request review

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `pullNumber`: Pull request number (number, required)

- **create_and_submit_pull_request_review** - Create and submit a review for a pull request without review comments

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `pullNumber`: Pull request number (number, required)
  - `body`: Review comment text (string, required)
  - `event`: Review action ('APPROVE', 'REQUEST_CHANGES', 'COMMENT') (string, required)
  - `commitID`: SHA of commit to review (string, optional)

- **create_pull_request** - Create a new pull request

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `title`: PR title (string, required)
  - `body`: PR description (string, optional)
  - `head`: Branch containing changes (string, required)
  - `base`: Branch to merge into (string, required)
  - `draft`: Create as draft PR (boolean, optional)
  - `maintainer_can_modify`: Allow maintainer edits (boolean, optional)

- **update_pull_request** - Update an existing pull request in a GitHub repository

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `pullNumber`: Pull request number to update (number, required)
  - `title`: New title (string, optional)
  - `body`: New description (string, optional)
  - `state`: New state ('open' or 'closed') (string, optional)
  - `base`: New base branch name (string, optional)
  - `maintainer_can_modify`: Allow maintainer edits (boolean, optional)

- **request_copilot_review** - Request a GitHub Copilot review for a pull request (experimental; subject to GitHub API support)

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `pullNumber`: Pull request number (number, required)
  - _Note_: Currently, this tool will only work for github.com

### Projects

- **list_projects** - List projects for a user or organization
  - `owner`: Owner login (string, required)
  - `owner_type`: Owner type ('user' or 'organization', optional)

- **get_project_fields** - Get fields for a project
  - `owner`: Owner login (string, required)
  - `owner_type`: Owner type ('user' or 'organization', optional)
  - `number`: Project number (number, required)

- **get_project_items** - Get items for a project
  - `owner`: Owner login (string, required)
  - `owner_type`: Owner type ('user' or 'organization', optional)
  - `number`: Project number (number, required)

- **create_project_issue** - Create a new issue in a repository
  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `title`: Issue title (string, required)
  - `body`: Issue body (string, optional)

- **add_issue_to_project** - Add an issue to a project
  - `project_id`: Project node ID (string, required)
  - `issue_id`: Issue node ID (string, required)

- **update_project_item_field** - Update a project item field value
  - `project_id`: Project node ID (string, required)
  - `item_id`: Item node ID (string, required)
  - `field_id`: Field node ID (string, required)
  - `text_value`: New text value (string, optional)

- **create_draft_issue** - Create a draft issue in a project
  - `project_id`: Project node ID (string, required)
  - `title`: Draft issue title (string, required)
  - `body`: Draft issue body (string, optional)

- **delete_project_item** - Delete an item from a project
  - `project_id`: Project node ID (string, required)
  - `item_id`: Item node ID (string, required)

### Repositories

- **create_or_update_file** - Create or update a single file in a repository
  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `path`: File path (string, required)
  - `message`: Commit message (string, required)
  - `content`: File content (string, required)
  - `branch`: Branch name (string, optional)
  - `sha`: File SHA if updating (string, optional)

- **delete_file** - Delete a file from a GitHub repository
  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `path`: Path to the file to delete (string, required)
  - `message`: Commit message (string, required)
  - `branch`: Branch to delete the file from (string, required)

- **list_branches** - List branches in a GitHub repository
  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `page`: Page number (number, optional)
  - `perPage`: Results per page (number, optional)

- **push_files** - Push multiple files in a single commit
  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `branch`: Branch to push to (string, required)
  - `files`: Files to push, each with path and content (array, required)
  - `message`: Commit message (string, required)

- **search_repositories** - Search for GitHub repositories
  - `query`: Search query (string, required)
  - `sort`: Sort field (string, optional)
  - `order`: Sort order (string, optional)
  - `page`: Page number (number, optional)
  - `perPage`: Results per page (number, optional)

- **create_repository** - Create a new GitHub repository
  - `name`: Repository name (string, required)
  - `description`: Repository description (string, optional)
  - `private`: Whether the repository is private (boolean, optional)
  - `autoInit`: Auto-initialize with README (boolean, optional)

- **get_file_contents** - Get contents of a file or directory
  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `path`: File path (string, required)
  - `ref`: Git reference (string, optional)

- **fork_repository** - Fork a repository
  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `organization`: Target organization name (string, optional)

- **create_branch** - Create a new branch
  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `branch`: New branch name (string, required)
  - `sha`: SHA to create branch from (string, required)

- **list_commits** - Get a list of commits of a branch in a repository
  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `sha`: Branch name, tag, or commit SHA (string, optional)
  - `path`: Only commits containing this file path (string, optional)
  - `page`: Page number (number, optional)
  - `perPage`: Results per page (number, optional)

- **get_commit** - Get details for a commit from a repository
  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `sha`: Commit SHA, branch name, or tag name (string, required)
  - `page`: Page number, for files in the commit (number, optional)
  - `perPage`: Results per page, for files in the commit (number, optional)

- **get_tag** - Get details about a specific git tag in a GitHub repository
  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `tag`: Tag name (string, required)

- **list_tags** - List git tags in a GitHub repository
  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `page`: Page number (number, optional)
  - `perPage`: Results per page (number, optional)

- **search_code** - Search for code across GitHub repositories
  - `query`: Search query (string, required)
  - `sort`: Sort field (string, optional)
  - `order`: Sort order (string, optional)
  - `page`: Page number (number, optional)
  - `perPage`: Results per page (number, optional)

### Users

- **search_users** - Search for GitHub users
  - `q`: Search query (string, required)
  - `sort`: Sort field (string, optional)
  - `order`: Sort order (string, optional)
  - `page`: Page number (number, optional)
  - `perPage`: Results per page (number, optional)

### Actions

- **list_workflows** - List workflows in a repository

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `page`: Page number (number, optional)
  - `perPage`: Results per page (number, optional)

- **list_workflow_runs** - List workflow runs for a specific workflow

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `workflow_id`: Workflow ID or filename (string, required)
  - `branch`: Filter by branch name (string, optional)
  - `event`: Filter by event type (string, optional)
  - `status`: Filter by run status (string, optional)
  - `page`: Page number (number, optional)
  - `perPage`: Results per page (number, optional)

- **run_workflow** - Trigger a workflow via workflow_dispatch event

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `workflow_id`: Workflow ID or filename (string, required)
  - `ref`: Git reference (branch, tag, or SHA) (string, required)
  - `inputs`: Input parameters for the workflow (object, optional)

- **get_workflow_run** - Get details of a specific workflow run

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `run_id`: Workflow run ID (number, required)

- **get_workflow_run_logs** - Download logs for a workflow run

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `run_id`: Workflow run ID (number, required)

- **list_workflow_jobs** - List jobs for a workflow run

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `run_id`: Workflow run ID (number, required)
  - `filter`: Filter by job status (string, optional)
  - `page`: Page number (number, optional)
  - `perPage`: Results per page (number, optional)

- **get_job_logs** - Download logs for a specific workflow job or efficiently get all failed job logs for a workflow run

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `job_id`: Job ID (number, required for single job logs)
  - `run_id`: Workflow run ID (number, required when using failed_only)
  - `failed_only`: When true, gets logs for all failed jobs in run_id (boolean, optional)
  - `return_content`: Returns actual log content instead of URLs (boolean, optional)

- **rerun_workflow_run** - Re-run an entire workflow

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `run_id`: Workflow run ID (number, required)
  - `enable_debug_logging`: Enable debug logging for the re-run (boolean, optional)

- **rerun_failed_jobs** - Re-run only the failed jobs in a workflow run

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `run_id`: Workflow run ID (number, required)
  - `enable_debug_logging`: Enable debug logging for the re-run (boolean, optional)

- **cancel_workflow_run** - Cancel a running workflow

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `run_id`: Workflow run ID (number, required)

- **list_workflow_run_artifacts** - List artifacts from a workflow run

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `run_id`: Workflow run ID (number, required)
  - `page`: Page number (number, optional)
  - `perPage`: Results per page (number, optional)

- **download_workflow_run_artifact** - Get download URL for a specific artifact

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `artifact_id`: Artifact ID (number, required)

- **delete_workflow_run_logs** - Delete logs for a workflow run

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `run_id`: Workflow run ID (number, required)

- **get_workflow_run_usage** - Get usage metrics for a workflow run

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `run_id`: Workflow run ID (number, required)

### Code Scanning

- **get_code_scanning_alert** - Get a code scanning alert

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `alertNumber`: Alert number (number, required)

- **list_code_scanning_alerts** - List code scanning alerts for a repository
  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `ref`: Git reference (string, optional)
  - `state`: Alert state (string, optional)
  - `severity`: Alert severity (string, optional)
  - `tool_name`: The name of the tool used for code scanning (string, optional)

### Secret Scanning

- **get_secret_scanning_alert** - Get a secret scanning alert

  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `alertNumber`: Alert number (number, required)

- **list_secret_scanning_alerts** - List secret scanning alerts for a repository
  - `owner`: Repository owner (string, required)
  - `repo`: Repository name (string, required)
  - `state`: Alert state (string, optional)
  - `secret_type`: The secret types to be filtered for in a comma-separated list (string, optional)
  - `resolution`: The resolution status (string, optional)

### Notifications

- **list_notifications** – List notifications for a GitHub user
  - `filter`: Filter to apply to the response (`default`, `include_read_notifications`, `only_participating`)
  - `since`: Only show notifications updated after the given time (ISO 8601 format)
  - `before`: Only show notifications updated before the given time (ISO 8601 format)
  - `owner`: Optional repository owner (string)
  - `repo`: Optional repository name (string)
  - `page`: Page number (number, optional)
  - `perPage`: Results per page (number, optional)

- **get_notification_details** – Get detailed information for a specific GitHub notification
  - `notificationID`: The ID of the notification (string, required)

- **dismiss_notification** – Dismiss a notification by marking it as read or done
  - `threadID`: The ID of the notification thread (string, required)
  - `state`: The new state of the notification (`read` or `done`)

- **mark_all_notifications_read** – Mark all notifications as read
  - `lastReadAt`: Describes the last point that notifications were checked (optional, RFC3339/ISO8601 string, default: now)
  - `owner`: Optional repository owner (string)
  - `repo`: Optional repository name (string)

- **manage_notification_subscription** – Manage a notification subscription (ignore, watch, or delete) for a notification thread
  - `notificationID`: The ID of the notification thread (string, required)
  - `action`: Action to perform: `ignore`, `watch`, or `delete` (string, required)

- **manage_repository_notification_subscription** – Manage a repository notification subscription (ignore, watch, or delete)
  - `owner`: The account owner of the repository (string, required)
  - `repo`: The name of the repository (string, required)
  - `action`: Action to perform: `ignore`, `watch`, or `delete` (string, required)

## Resources

### Repository Content

- **Get Repository Content**
  Retrieves the content of a repository at a specific path.

  - **Template**: `repo://{owner}/{repo}/contents{/path*}`
  - **Parameters**:
    - `owner`: Repository owner (string, required)
    - `repo`: Repository name (string, required)
    - `path`: File or directory path (string, optional)

- **Get Repository Content for a Specific Branch**
  Retrieves the content of a repository at a specific path for a given branch.

  - **Template**: `repo://{owner}/{repo}/refs/heads/{branch}/contents{/path*}`
  - **Parameters**:
    - `owner`: Repository owner (string, required)
    - `repo`: Repository name (string, required)
    - `branch`: Branch name (string, required)
    - `path`: File or directory path (string, optional)

- **Get Repository Content for a Specific Commit**
  Retrieves the content of a repository at a specific path for a given commit.

  - **Template**: `repo://{owner}/{repo}/sha/{sha}/contents{/path*}`
  - **Parameters**:
    - `owner`: Repository owner (string, required)
    - `repo`: Repository name (string, required)
    - `sha`: Commit SHA (string, required)
    - `path`: File or directory path (string, optional)

- **Get Repository Content for a Specific Tag**
  Retrieves the content of a repository at a specific path for a given tag.

  - **Template**: `repo://{owner}/{repo}/refs/tags/{tag}/contents{/path*}`
  - **Parameters**:
    - `owner`: Repository owner (string, required)
    - `repo`: Repository name (string, required)
    - `tag`: Tag name (string, required)
    - `path`: File or directory path (string, optional)

- **Get Repository Content for a Specific Pull Request**
  Retrieves the content of a repository at a specific path for a given pull request.

  - **Template**: `repo://{owner}/{repo}/refs/pull/{prNumber}/head/contents{/path*}`
  - **Parameters**:
    - `owner`: Repository owner (string, required)
    - `repo`: Repository name (string, required)
    - `prNumber`: Pull request number (string, required)
    - `path`: File or directory path (string, optional)

## Library Usage

The exported Go API of this module should currently be considered unstable, and subject to breaking changes. In the future, we may offer stability; please file an issue if there is a use case where this would be valuable.

## License

This project is licensed under the terms of the MIT open source license. Please refer to [MIT](./LICENSE) for the full terms.
