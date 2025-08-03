# LangChain Prompts MCP Server

<div align="left">
  <img src="https://python.langchain.com/img/brand/wordmark.png" alt="LangChain" width="250" />
</div>

## Overview

A **Model Context Protocol (MCP) server** that provides seamless access to the [LangSmith](https://smith.langchain.com/) prompt library—the world's largest collection of community-vetted AI prompts. With over 1000+ battle-tested prompts, advanced search capabilities, and rich metadata including usage statistics and version history, this server transforms how you discover and integrate prompts into your AI workflows. Access professional-grade prompts through natural language queries, making prompt engineering instantly actionable across Claude Desktop, Claude Code, and other MCP-compatible clients.



## Background

Our MCP Server connects directly to [LangSmith](https://smith.langchain.com/), LangChain's official platform for prompt management and LLM application development. The server provides intelligent access to a vast ecosystem of prompts that have been created, tested, and refined by the AI community.

Core Capabilities:
- **Prompt Discovery**: Search and filter through thousands of public prompts by name, owner, description, or tags
- **Rich Metadata**: Access download counts, view statistics, likes, and community engagement metrics
- **Version Control**: Track prompt evolution with full version history and commit information
- **Template Intelligence**: Work with parameterized prompts including input/output schemas
- **Advanced Analytics**: Get library-wide statistics, trending prompts, and popularity metrics

LLM-Enhanced Features:
- **Intelligent Completions**: Context-aware prompt completion suggestions
- **Prompt Validation**: Automated quality checks and best practice validation
- **Similarity Search**: Find related prompts based on content and structure
- **Comparative Analysis**: Side-by-side prompt comparison with detailed insights

Authentication & Access:
- **Public Library**: Access thousands of community prompts without authentication
- **Private Prompts**: Authenticate with LangSmith API key for private prompt access
- **User Collections**: Browse prompts by specific creators and organizations



## MCP Client Configuration

### Known Client Compatibility:
- Claude Desktop
- Claude Code  
- OpenAI ChatGPT (via Custom Connectors)
- Cursor IDE
- Continue.dev
- VS Code (with MCP extension)

### Claude Desktop
```json
{
  "mcpServers": {
    "langchain-prompts": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.prompts.mcpcentral.io/mcp"],
      "env": {
        "LANGSMITH_API_KEY": "your-api-key-optional"
      }
    }
  }
}
```

### Claude Code
```
claude mcp add langchain-prompts -s user --transport http https://mcp.prompts.mcpcentral.io/mcp
```

### OpenAI ChatGPT (Custom Connectors)
Use the MCP endpoint URL: `https://mcp.prompts.mcpcentral.io/mcp`

### Cursor IDE & Continue.dev
```json
{
  "mcpServers": [
    {
      "name": "langchain-prompts",
      "url": "https://mcp.prompts.mcpcentral.io/mcp",
      "env": {
        "LANGSMITH_API_KEY": "your-api-key-optional"
      }
    }
  ]
}
```



## MCP Version Compatibility

### MCP 2025-06-18 Compliance
- **Protocol Version**: [2025-06-18](https://modelcontextprotocol.io/introduction) with full specification compliance
- **Structured Output**: Enhanced tools with comprehensive schemas
- **Resource Support**: Dynamic collections with real-time updates
- **Prompt Templates**: Guided workflows for prompt discovery and analysis
- **Title Fields**: All tools, resources, and prompts include descriptive titles
- **Transports**: stdio + Streamable HTTP with custom Workers transport

### Enhanced Compatibility
- **OpenAI Integration**: Compatible with ChatGPT Custom Connectors
- **Enterprise Ready**: Built-in rate limiting and security controls
- **Cloud Optimized**: Deployed on Cloudflare Workers for global availability

### Prompt Management Tools (13 Total)
- **List Prompts**: Browse public prompts with filtering and pagination
- **Search Prompts**: Advanced search with multiple filter criteria
- **Get Prompt**: Retrieve detailed prompt information including metadata
- **Get Prompt Statistics**: Access library-wide analytics and trends
- **Like/Unlike Prompt**: Engage with community prompts (requires auth)
- **Get Prompt Versions**: Track prompt evolution and changes
- **Get User Prompts**: Browse prompts by specific creators
- **Get Popular Prompts**: Discover trending and high-engagement prompts
- **Get Prompt Content**: Access actual prompt templates and schemas
- **Compare Prompts**: Analyze multiple prompts side-by-side
- **Validate Prompt**: Check prompt quality and best practices
- **Get Prompt Completions**: Intelligent auto-completion suggestions

### Dynamic Resources (3 Total)
- **Popular Prompts Collection**: Real-time trending prompts
- **Recent Prompts Collection**: Latest community contributions
- **Trending Prompts Collection**: Engagement-based recommendations

### Guided Prompts (4 Total)
- **Analyze Prompt**: Comprehensive prompt effectiveness analysis
- **Discover Prompts**: Guided exploration of the prompt library
- **Find Similar Prompts**: Discover related prompts by similarity
- **Improve Prompt**: Get suggestions for prompt enhancement



## Available Tools

| Tool | Name | Description | Parameters |
|------|------|-------------|------------|
| **List Prompts** | `list_prompts` | List public prompts from LangSmith with optional filtering | `limit`, `owner`, `search` |
| **Get Prompt** | `get_prompt` | Get detailed information about a specific prompt | `prompt_name` |
| **Get Prompt Statistics** | `get_prompt_statistics` | Get statistics about the prompt library | None |
| **Search Prompts** | `search_prompts` | Advanced search for prompts with comprehensive filtering | `query`, `owner`, `tags`, `is_public`, `min_likes`, `min_downloads`, `sort_by`, `sort_order`, `limit` |
| **Like Prompt** | `like_prompt` | Like a specific prompt (requires authentication) | `prompt_name` |
| **Unlike Prompt** | `unlike_prompt` | Remove like from a specific prompt (requires authentication) | `prompt_name` |
| **Get Prompt Versions** | `get_prompt_versions` | Get version history and commits for a specific prompt | `prompt_name`, `limit` |
| **Get User Prompts** | `get_user_prompts` | Get prompts created by a specific user | `username`, `include_private`, `limit` |
| **Get Popular Prompts** | `get_popular_prompts` | Get trending and popular prompts | `time_period`, `category`, `limit` |
| **Get Prompt Content** | `get_prompt_content` | Get the actual prompt template content and configuration | `prompt_name`, `version`, `include_model_config` |
| **Compare Prompts** | `compare_prompts` | Compare multiple prompts side by side | `prompt_names`, `comparison_criteria` |
| **Validate Prompt** | `validate_prompt` | Validate prompt structure and quality | `prompt_name`, `check_completeness`, `check_best_practices` |
| **Get Prompt Completions** | `get_prompt_completions` | Get intelligent auto-completions for prompt templates | `partial_text`, `context`, `max_suggestions` |

## Available Resources

| Resource | URI | Description |
|----------|-----|-------------|
| **Popular Prompts Collection** | `langsmith://collections/popular` | Collection of trending and popular prompts |
| **Recent Prompts Collection** | `langsmith://collections/recent` | Recently updated prompts |
| **Trending Prompts Collection** | `langsmith://collections/trending` | Prompts trending by engagement |

## Available Prompts

| Prompt | Name | Description | Arguments |
|--------|------|-------------|-----------|
| **Analyze Prompt** | `analyze-prompt` | Analyze prompt effectiveness, structure, and areas for improvement | `prompt_content` (required), `analysis_depth` (optional), `target_audience` (optional) |
| **Discover Prompts** | `discover-prompts` | Discover prompts based on use case, domain, or specific requirements | `use_case` (optional), `domain` (optional), `requirements` (optional) |
| **Find Similar Prompts** | `find-similar-prompts` | Find prompts similar to a given example or description | `reference_prompt` (optional), `similarity_criteria` (optional), `limit` (optional) |
| **Improve Prompt** | `improve-prompt` | Get suggestions to improve an existing prompt | `prompt_content` (required), `improvement_goals` (optional), `target_model` (optional) |



## Architecture

### Key Technical Features
- **Dual Transport Design**: stdio for local development, HTTP for production
- **Custom Workers Transport**: Optimized for Cloudflare Workers (54% smaller than standard)
- **Type Safety**: Full TypeScript implementation with runtime validation
- **Intelligent Caching**: Multi-tier caching for optimal performance
- **Rate Limiting**: Built-in protection with configurable limits
- **Security First**: Input validation, injection protection, and secure error handling

### Performance Optimizations
- **Bundle Size**: 507KB optimized bundle for serverless deployment
- **Cold Start**: Minimal latency with Worker-optimized initialization
- **Cache Strategy**: LRU caching with TTL for frequently accessed prompts
- **Retry Logic**: Exponential backoff with jitter for resilient API calls



## Data Overview

### Primary Data Source: LangSmith Prompt Hub
- **Content**: 1000+ community-vetted prompts from [smith.langchain.com](https://smith.langchain.com)
- **Metadata**: Download counts, view statistics, likes, tags, and version history
- **Templates**: Parameterized prompts with input/output schemas
- **Updates**: Real-time access to latest community contributions
- **Privacy**: Public prompts accessible without auth, private with API key



## Version Information

- **Version**: 1.0.0
- **Protocol**: MCP 2025-06-18 
- **SDK**: @modelcontextprotocol/sdk 1.16.0
- **Features**: Full specification compliance with resources, prompts, and structured output
- **Transports**: 
  - **stdio**: Default MCP transport for direct client integration
  - **http**: MCP 2025-06-18 Streamable HTTP with header validation

## Testing

- **MCP Central Lab**: Test the server interactively at https://lab.mcpcentral.io/

## MCP Registry

This server is published in the official [Model Context Protocol Registry](https://github.com/modelcontextprotocol/registry). The registry configuration enables:

- **Server Discovery**: Automatic detection by MCP-compatible clients
- **Remote Access**: HTTP transport endpoint at `https://mcp.prompts.mcpcentral.io/mcp`
- **Package Distribution**: Available via npx for instant access
- **Client Compatibility**: Verified support for Claude Desktop, Claude Code, and more
- **Feature Declaration**: 13 tools, 3 resources, 4 prompts with advanced search capabilities

## Support

- **Documentation**: [MCP Documentation](https://modelcontextprotocol.io/docs)
- **LangSmith**: [LangSmith Platform](https://smith.langchain.com)
- **Health Check**: `GET https://mcp.prompts.mcpcentral.io/health` for status monitoring

---

## Working Examples

### Example 1: Prompt Discovery for Developers

**Scenario**: A developer wants to find the best prompts for code review and documentation.

**Tools Used**: `search_prompts`, `get_prompt_content`, `compare_prompts`

1. **Search for Code Review Prompts**: Use search_prompts with query "code review"
2. **Get Template Details**: Retrieve full content for top results
3. **Compare Options**: Use compare_prompts to analyze differences

**Expected Results**: Curated code review prompts with templates, best practices, and community ratings.

### Example 2: Building a Prompt Library for Your Team

**Scenario**: A team lead wants to standardize prompts across their organization.

**Tools Used**: `get_popular_prompts`, `validate_prompt`, `get_prompt_versions`

1. **Discover Popular Prompts**: Get trending prompts in your domain
2. **Validate Quality**: Check prompts against best practices
3. **Track Changes**: Monitor version history for selected prompts

**Expected Results**: Validated, high-quality prompts with version control for team standardization.

### Example 3: AI Assistant Enhancement

**Scenario**: An AI engineer wants to improve their assistant's response quality.

**Tools Used**: `analyze-prompt`, `find-similar-prompts`, `improve-prompt`

1. **Analyze Current Prompts**: Use the analyze-prompt workflow
2. **Find Better Alternatives**: Discover similar high-performing prompts
3. **Get Improvement Suggestions**: Use improve-prompt for optimization

**Expected Results**: Enhanced prompts with measurable improvements in response quality and consistency.

### Example 4: Research and Experimentation

**Scenario**: A researcher needs to understand prompt engineering patterns across different use cases.

**Tools Used**: `get_prompt_statistics`, `list_prompts`, `get_user_prompts`

1. **Analyze Library Statistics**: Understand overall trends and patterns
2. **Browse by Category**: Explore prompts across different domains
3. **Study Expert Contributions**: Examine prompts from top creators

**Expected Results**: Comprehensive understanding of prompt patterns, trends, and best practices in the community.
