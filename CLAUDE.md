# Main claude.md file

Preferences across all projects.

## Architecture
- This is an AWS shop. The only cloud I prefer to use.
- go with boto3 clients when possible. Resources will do in a pinch.
- Default database is DynamoDB. Work with the Dynamo MCP.

## Docker
- Use ghcr.io (GitHub Container Registry) for all image registries.
- Use multi-stage builds when they provide significant final image size reduction.

## Kubernetes
- Use Helm formats with YAML files for manifests.
- Combine multiple spec files into a single file when they relate to a single project.
- Virginia.edu K8S cluster: ONLY deploy to the `uvasds-services` namespace.
- Deployment strategy: launch new tagged versions and roll them out as new versioned deployments.

## DevOps & CI/CD
- Use GitHub Actions for all CI/CD pipelines.
- Use CloudFormation for AWS cloud deployments.

## Bash Scripts
- Use `set -e` for error handling in all scripts.
- Output should go to stdout/screen only (no file logging from scripts themselves).

## Conventions & AI Guidance
- All endpoints return typed Pydantic models
- Never commit directly to main
- Keep external classes to a minimum, i.e. don't create too many separate files.
- If this is a python project it should use pipenv to create and activate a virtual
  environment. That means it uses "pipenv install" to add new packages.
- If you create any temporary new files, scripts, or helper files for iteration, 
  clean up these files by removing them at the end of the task.
- ALWAYS read and understand relevant files before proposing code edits. Do not speculate about code you have not inspected. If the user references a specific file/path, you MUST open and inspect it before explaining or proposing fixes. Be rigorous and persistent in searching code for key facts. Thoroughly review the style, conventions, and abstractions of the codebase before implementing new features or abstractions.
- After receiving tool results, carefully reflect on their quality and determine optimal next steps before proceeding. Use your thinking to plan and iterate based on this new information, and then take the best next action.
- After completing a task that involves tool use, provide a quick summary of what you've done.
- For maximum efficiency, whenever you need to perform multiple independent operations, invoke all relevant tools simultaneously rather than sequentially.
- Before you finish, please verify your solution
- Do what has been asked; nothing more, nothing less.
- NEVER create files unless they're absolutely necessary for achieving your goal.
- ALWAYS prefer editing an existing file to creating a new one
- NEVER proactively create documentation files (*.md) or README files unless explicitly requested
- NEVER save working files, text/mds, or tests to the root folder
- Never continuously check status after spawning a swarm — wait for results
- ALWAYS read a file before editing it
- NEVER commit secrets, credentials, or .env files

## Testing & Logging
- Use pytest for all test frameworks.
- Use the Python logging package for application logging.
- Start with log level WARNING by default.
- Use docker-compose for local testing environments when applicable.

<investigate_before_answering> Never speculate about code you have not opened. If the user references a specific file, you MUST read the file before answering. Make sure to investigate and read relevant files BEFORE answering questions about the codebase. Never make any claims about code before investigating unless you are certain of the correct answer - give grounded and hallucination-free answers. </investigate_before_answering>

<do_not_act_before_instructions> Do not jump into implementatation or changes files unless clearly instructed to make changes. When the user's intent is ambiguous, default to providing information, doing research, and providing recommendations rather than taking action. Only proceed with edits, modifications, or implementations when the user explicitly requests them. </do_not_act_before_instructions>

<use_parallel_tool_calls> If you intend to call multiple tools and there are no dependencies between the tool calls, make all of the independent tool calls in parallel. Prioritize calling tools simultaneously whenever the actions can be done in parallel rather than sequentially. For example, when reading 3 files, run 3 tool calls in parallel to read all 3 files into context at the same time. Maximize use of parallel tool calls where possible to increase speed and efficiency. However, if some tool calls depend on previous calls to inform dependent values like the parameters, do NOT call these tools in parallel and instead call them sequentially. Never use placeholders or guess missing parameters in tool calls. </use_parallel_tool_calls>

## Security Rules
- NEVER hardcode API keys, secrets, or credentials in source files
- NEVER commit .env files or any file containing secrets
- Always validate user input at system boundaries
- Always sanitize file paths to prevent directory traversal
- Run npx @claude-flow/cli@latest security scan after security-related changes
