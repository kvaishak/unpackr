# Changelog

## [Initial Release] - {PR_MERGE_DATE}

### Added

- **Universal ZIP Merging**: Merge multiple ZIP files into a single organized folder
- **Intelligent Structure Detection**: Automatically detects Google Takeout archives or regular ZIP files
- **Smart Deduplication**: SHA256-based duplicate file detection and automatic skipping
- **Conflict Resolution**: Automatically renames files with same name but different content (e.g., `photo.jpg` → `photo (1).jpg`)
- **Root Folder Unwrapping**: Automatically unwraps single-root-folder structures common in ZIP files
- **macOS Metadata Filtering**: Automatically filters out `__MACOSX`, `.DS_Store`, and other hidden files
- **Configurable Output**: Specify a custom subfolder name for merged contents
- **Progress Tracking**: Real-time toast notifications showing merge progress and statistics
- **Error Recovery**: Continues processing remaining files if individual files fail
- **Customizable Filter**: Filter ZIP files by name pattern (e.g., "takeout-", "photos", etc.)
- **Optional ZIP Deletion**: Optionally delete original ZIP files after successful merge
- **Cross-Device Support**: Handles file moves across different file systems
- **Google Takeout Support**: Special handling for Google Takeout archive structure
- **Preferences**: Configurable default input and output folders

### Features

- Merge any number of ZIP files with a single command
- Preserves internal folder structure from ZIP files
- Handles nested single-directory structures (unwraps automatically)
- Works with single or multiple ZIP files
- Supports mixed ZIP types (Google Takeout + regular ZIPs in same batch)
- Directory validation before processing
- Comprehensive error messages with context
- Safe defaults (preserves original files unless explicitly deleted)

### Technical Details

- Built with TypeScript for type safety
- Uses yauzl for robust ZIP extraction
- Streaming file operations for memory efficiency
- Recursive hash caching for performance
- Comprehensive input validation
- Path security (prevents directory traversal attacks)
