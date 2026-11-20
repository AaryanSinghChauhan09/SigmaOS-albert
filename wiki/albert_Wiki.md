# SigmaOS-albert Component Wiki

## Overview
SigmaOS-albert provides Albert launcher and application search support for the SigmaOS operating system. It demonstrates the application launcher subsystem and quick access within the SigmaOS ecosystem, following the principles of clear abstraction and deterministic launcher initialization.

## Principles
- Single Responsibility
- Launcher Abstraction
- Fail-Fast on Launcher Initialization Errors
- Deterministic Launcher Setup
- Clear Abstraction Over Launcher APIs
- Composition over Inheritance for launcher extensions

## Architecture
SigmaOS-albert follows a launcher pattern:
- **Launcher Core**: Provides application search, quick access, and launcher initialization
- **Application Search**: Supports fuzzy search, application matching, and result ranking
- **Quick Access**: Supports pinned applications, recent applications, and frequent applications
- **Error Handling**: Fail-fast on invalid launcher configurations or unsupported launcher types

## API
The component provides the following public APIs:
- `launcher::search(query)` - Search for applications by given query
- `launcher::launch(application)` - Launch an application by name or ID
- `launcher::pin::application(application)` - Pin an application for quick access
- `launcher::status::available()` - Get launcher status and available applications
- Error types for launcher failure scenarios or unsupported launcher types

## Test Structure (Arrange-Act-ASSERT)
All tests follow the AAA pattern:
1. **Arrange**: Set up test environment with specific launcher configuration
2. **Act**: Execute the code under test (application search, application launch)
3. **Assert**: Verify the expected launcher results

Example:
```rust
#[test]
fn test_launcher_search_aaa() {
    // Arrange
    let query = "text editor";
    
    // Act
    let result = launcher::search(query);
    
    // Assert
    assert!(result.is_ok());
    let results = result.unwrap();
    assert!(!results.is_empty());
}
```

## Development
- Follows Rust best practices with `#![forbid(unsafe_code)]`
- Launcher initialization is best-effort; gracefully degrades on unsupported configurations
- Comprehensive error types for all launcher failure scenarios
- Unit tests provided for application search and application launch
- Integration tests for full launcher system with actual application integration

## TODO
- Add support for additional search features (fuzzy search, boolean search, search filtering)
- Expand quick access capabilities (pinned applications, recent applications, frequency tracking)
- Add launcher customization (appearance, hotkeys, appearance themes)
- Create integration tests with actual application launcher systems
- Implement launcher persistence and application history features