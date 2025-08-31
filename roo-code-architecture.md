# Roo Code VSCode Extension Architecture

This Mermaid diagram shows the architectural structure of the Roo Code VSCode extension's `src` directory, illustrating the relationships between different components, services, and integrations.

```mermaid
graph TB
    %% Main Extension Entry Point
    EXT[extension.ts<br/>📱 Main Extension Entry]

    %% Core Architecture Layer
    subgraph CORE ["🧠 Core Layer"]
        TASK[task/<br/>📋 Task Management]
        TOOLS[tools/<br/>🔧 Tool System]
        CONFIG[config/<br/>⚙️ Configuration]
        WEBVIEW[webview/<br/>🖥️ Webview Controller]
        PROMPTS[prompts/<br/>💬 Prompt Templates]
        CONTEXT[context-tracking/<br/>📊 Context Management]
        DIFF[diff/<br/>🔄 Diff Processing]
        PROTECT[protect/<br/>🛡️ Protection Layer]
        CONDENSE[condense/<br/>📦 Content Condensing]
        MENTIONS[mentions/<br/>@️⃣ Mention System]
        CHECKPOINTS[checkpoints/<br/>💾 Checkpoint System]
        IGNORE[ignore/<br/>🚫 Ignore Rules]
        SLIDING[sliding-window/<br/>🪟 Context Window]
        ASSIST[assistant-message/<br/>🤖 Assistant Messages]
        PERSIST[task-persistence/<br/>💿 Task Persistence]
        ENV[environment/<br/>🌍 Environment Config]
    end

    %% API Layer
    subgraph API ["🔌 API Layer"]
        PROVIDERS[providers/<br/>🤖 AI Providers]
        TRANSFORM[transform/<br/>🔄 Data Transform]
        API_INDEX[index.ts<br/>📡 API Entry Point]
    end

    %% AI Providers Detail
    subgraph PROVIDERS_DETAIL ["🤖 AI Providers"]
        ANTHROPIC[anthropic.ts<br/>🧠 Claude]
        OPENAI[openai.ts<br/>🤖 GPT Models]
        GEMINI[gemini.ts<br/>💎 Google Gemini]
        OLLAMA[ollama.ts<br/>🦙 Local Models]
        GROQ[groq.ts<br/>⚡ Groq]
        BEDROCK[bedrock.ts<br/>☁️ AWS Bedrock]
        VERTEX[vertex.ts<br/>🏔️ Google Vertex]
        MISTRAL[mistral.ts<br/>🌪️ Mistral AI]
        OTHERS[+ 20 more providers<br/>🌐 Various APIs]
    end

    %% Tools Detail
    subgraph TOOLS_DETAIL ["🔧 Available Tools"]
        READ_FILE[readFileTool.ts<br/>📖 File Reading]
        WRITE_FILE[writeToFileTool.ts<br/>✍️ File Writing]
        SEARCH[searchFilesTool.ts<br/>🔍 File Search]
        EXECUTE[executeCommandTool.ts<br/>⚡ Command Execution]
        BROWSER[browserActionTool.ts<br/>🌐 Browser Automation]
        DIFF_TOOL[applyDiffTool.ts<br/>🔄 Diff Application]
        CODEBASE[codebaseSearchTool.ts<br/>🔍 Code Search]
        MCP_TOOL[useMcpToolTool.ts<br/>🔗 MCP Integration]
        COMPLETION[attemptCompletionTool.ts<br/>✅ Task Completion]
        FOLLOWUP[askFollowupQuestionTool.ts<br/>❓ Follow-up Questions]
        TODO[updateTodoListTool.ts<br/>📝 Todo Management]
        MODE[switchModeTool.ts<br/>🔄 Mode Switching]
    end

    %% Services Layer
    subgraph SERVICES ["🛠️ Services Layer"]
        BROWSER_SVC[browser/<br/>🌐 Browser Service]
        MCP[mcp/<br/>🔗 Model Context Protocol]
        SEARCH_SVC[search/<br/>🔍 Search Service]
        RIPGREP[ripgrep/<br/>🔎 Fast Text Search]
        TREE_SITTER[tree-sitter/<br/>🌳 Code Parsing]
        CODE_INDEX[code-index/<br/>📚 Code Indexing]
        GLOB_SVC[glob/<br/>🗂️ File Matching]
        COMMAND_SVC[command/<br/>⚡ Command Service]
        MARKETPLACE[marketplace/<br/>🏪 Extension Marketplace]
        ROO_CONFIG[roo-config/<br/>⚙️ Roo Configuration]
        MDM[mdm/<br/>📱 Device Management]
        CHECKPOINT_SVC[checkpoints/<br/>💾 Checkpoint Service]
    end

    %% Integrations Layer
    subgraph INTEGRATIONS ["🔌 VSCode Integrations"]
        EDITOR_INT[editor/<br/>📝 Editor Integration]
        TERMINAL_INT[terminal/<br/>💻 Terminal Integration]
        WORKSPACE_INT[workspace/<br/>📁 Workspace Integration]
        DIAGNOSTICS[diagnostics/<br/>🩺 Diagnostics Integration]
        THEME_INT[theme/<br/>🎨 Theme Integration]
        CLAUDE_CODE[claude-code/<br/>🧠 Claude Code Integration]
        MISC_INT[misc/<br/>🔧 Misc Integrations]
    end

    %% Shared Components
    subgraph SHARED ["📚 Shared Components"]
        UTILS[utils/<br/>🛠️ Utilities]
        SHARED_TYPES[shared/<br/>📋 Shared Types]
        I18N[i18n/<br/>🌐 Internationalization]
    end

    %% UI Layer
    subgraph UI ["🖼️ UI Layer"]
        WEBVIEW_UI[webview-ui/<br/>⚛️ React Frontend]
        ACTIVATE[activate/<br/>🚀 Activation Logic]
    end

    %% Testing & Build
    subgraph BUILD ["🏗️ Build & Test"]
        TESTS[__tests__/<br/>🧪 Test Suite]
        MOCKS[__mocks__/<br/>🎭 Test Mocks]
        WORKERS[workers/<br/>👷 Background Workers]
    end

    %% Connections - Main Flow
    EXT --> CORE
    EXT --> API
    EXT --> SERVICES
    EXT --> INTEGRATIONS
    EXT --> SHARED
    EXT --> UI

    %% Core Internal Connections
    TASK --> TOOLS
    TASK --> PERSIST
    TASK --> CHECKPOINTS
    WEBVIEW --> TASK
    TOOLS --> CONTEXT
    TOOLS --> PROTECT
    DIFF --> TOOLS
    CONDENSE --> SLIDING

    %% API Connections
    API_INDEX --> PROVIDERS
    PROVIDERS --> PROVIDERS_DETAIL
    ANTHROPIC --> TRANSFORM
    OPENAI --> TRANSFORM
    GEMINI --> TRANSFORM
    OLLAMA --> TRANSFORM

    %% Tools Connections
    TOOLS --> TOOLS_DETAIL
    READ_FILE --> PROTECT
    WRITE_FILE --> PROTECT
    EXECUTE --> COMMAND_SVC
    BROWSER --> BROWSER_SVC
    CODEBASE --> CODE_INDEX
    MCP_TOOL --> MCP

    %% Services Connections
    SEARCH_SVC --> RIPGREP
    CODE_INDEX --> TREE_SITTER
    BROWSER_SVC --> BROWSER
    CHECKPOINT_SVC --> CHECKPOINTS

    %% Integration Connections
    EDITOR_INT --> TASK
    TERMINAL_INT --> EXECUTE
    WORKSPACE_INT --> SEARCH_SVC
    DIAGNOSTICS --> CODE_INDEX

    %% UI Connections
    WEBVIEW_UI --> WEBVIEW
    ACTIVATE --> EXT

    %% Shared Connections
    UTILS --> CORE
    UTILS --> SERVICES
    SHARED_TYPES --> API
    I18N --> UI

    %% Styling
    classDef coreClass fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    classDef apiClass fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    classDef serviceClass fill:#e8f5e8,stroke:#1b5e20,stroke-width:2px
    classDef integrationClass fill:#fff3e0,stroke:#e65100,stroke-width:2px
    classDef uiClass fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    classDef sharedClass fill:#f1f8e9,stroke:#33691e,stroke-width:2px
    classDef buildClass fill:#efebe9,stroke:#3e2723,stroke-width:2px
    classDef toolClass fill:#e0f2f1,stroke:#004d40,stroke-width:2px
    classDef providerClass fill:#f8bbd9,stroke:#ad1457,stroke-width:2px

    class TASK,TOOLS,CONFIG,WEBVIEW,PROMPTS,CONTEXT,DIFF,PROTECT,CONDENSE,MENTIONS,CHECKPOINTS,IGNORE,SLIDING,ASSIST,PERSIST,ENV coreClass
    class API_INDEX,PROVIDERS,TRANSFORM apiClass
    class BROWSER_SVC,MCP,SEARCH_SVC,RIPGREP,TREE_SITTER,CODE_INDEX,GLOB_SVC,COMMAND_SVC,MARKETPLACE,ROO_CONFIG,MDM,CHECKPOINT_SVC serviceClass
    class EDITOR_INT,TERMINAL_INT,WORKSPACE_INT,DIAGNOSTICS,THEME_INT,CLAUDE_CODE,MISC_INT integrationClass
    class WEBVIEW_UI,ACTIVATE uiClass
    class UTILS,SHARED_TYPES,I18N sharedClass
    class TESTS,MOCKS,WORKERS buildClass
    class READ_FILE,WRITE_FILE,SEARCH,EXECUTE,BROWSER,DIFF_TOOL,CODEBASE,MCP_TOOL,COMPLETION,FOLLOWUP,TODO,MODE toolClass
    class ANTHROPIC,OPENAI,GEMINI,OLLAMA,GROQ,BEDROCK,VERTEX,MISTRAL,OTHERS providerClass
```

## Architecture Overview

### 🏗️ **Core Components**

1. **Task Management System** - Handles AI agent tasks and workflow
2. **Tool System** - Provides 20+ tools for file operations, code analysis, browser automation, etc.
3. **Context Management** - Tracks conversation context and sliding window
4. **Protection Layer** - Ensures safe file operations and prevents harmful actions

### 🤖 **AI Provider Support**

The extension supports **25+ AI providers** including:

- **Anthropic Claude** (multiple versions)
- **OpenAI GPT** models
- **Google Gemini & Vertex AI**
- **Local models** via Ollama, LM Studio
- **Cloud providers** like AWS Bedrock, Groq, Mistral
- **Specialized providers** for different use cases

### 🔧 **Rich Tool Ecosystem**

- **File Operations**: Read, write, search files
- **Code Analysis**: Codebase search, syntax parsing
- **Browser Automation**: Web interaction capabilities
- **Command Execution**: Terminal command execution
- **MCP Integration**: Model Context Protocol support
- **Task Management**: Todo lists, checkpoints, completion tracking

### 🔌 **Deep VSCode Integration**

- **Editor Integration**: Direct code manipulation
- **Terminal Integration**: Command execution
- **Workspace Integration**: Project-wide operations
- **Diagnostics Integration**: Error detection and fixing
- **Theme Integration**: UI consistency

### ⚛️ **Modern Architecture**

- **React-based UI** with modern component architecture
- **Service-oriented design** with clear separation of concerns
- **Extensible plugin system** via MCP
- **Comprehensive testing** with mocks and test utilities
- **Internationalization** support for global users

This architecture enables Roo Code to function as a powerful AI-powered coding assistant with deep VSCode integration and extensive tool capabilities.
