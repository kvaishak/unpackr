# Changelog

All notable changes to Unpackr will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2024-11-22

### Added
- **ZIP Merging Engine**: Core functionality to merge multiple ZIP files into a single organized folder
- **Smart Deduplication**: SHA256-based duplicate file detection and automatic skipping
- **Conflict Resolution**: Automatically renames files with same name but different content (e.g., `photo.jpg` → `photo (1).jpg`)
- **Progress Tracking**: Real-time toast notifications showing merge progress and statistics
- **Customizable Filter**: Filter ZIP files by name pattern (e.g., "takeout-", "photos", etc.)
- **Optional ZIP Deletion**: Optionally delete original ZIP files after successful merge
- **Preferences**: Configurable default input and output folders
- **Google Takeout Support**: Initial support designed for Google Takeout archive structure

### Technical
- Built with TypeScript for type safety
- Uses yauzl for robust ZIP extraction
- Streaming file operations for memory efficiency
- SHA256 hash caching for performance
- Comprehensive input validation
- Path security (prevents directory traversal attacks)

---

## [1.1.0] - 2024-11-22

### Added
- **Universal ZIP Support**: Extended beyond Google Takeout to work with ANY ZIP files
- **Intelligent Structure Detection**: Automatically detects Google Takeout archives vs regular ZIP files

### Changed
- Renamed command from "Merge Google Takeout Files" to "Merge ZIP Files" for broader appeal
- Made dual-mode processing (Google Takeout + regular ZIPs work seamlessly)

### Fixed
- Extension now processes regular photo collections, backups, and any ZIP batches

---

## [1.2.0] - 2024-11-22

### Fixed
- **Multiple ZIP Merge Issue**: Fixed bug where multiple ZIPs created separate folders instead of merging into one
- **Root Folder Unwrapping**: Fixed issue where single-root-folder ZIPs weren't being properly unwrapped
- **macOS Metadata Handling**: Fixed root folder detection when `__MACOSX` metadata folders were present

### Added
- **macOS Metadata Filtering**: Automatically filters out `__MACOSX`, `.DS_Store`, and hidden files
- **Root Folder Unwrapping**: Automatically unwraps single-root-folder structures common in ZIP files

### Technical
- Improved subdirectory detection algorithm
- Recursive unwrapping for nested single-directory structures
- Metadata filtering during extraction and processing

---

## [1.3.0] - 2024-11-22

### Added
- **Output Folder Naming**: Option to specify a custom subfolder name for merged contents
- **Zip Bomb Protection**: Safe Mode (enabled by default) detects suspicious archives with high compression ratios (>100x) and size limits (>100GB)
- **Cross-Device Support**: Handles file moves across different file systems (EXDEV error handling)
- **Error Recovery**: Continues processing remaining files if individual files fail

### Security
- Zip bomb detection with compression ratio checks
- Total uncompressed size limit checks
- Safe Mode enabled by default

---

## [1.4.0] - 2024-11-22 (Pre-Release)

### Changed
- **Removed 100GB Size Limit**: Removed arbitrary size limit to allow processing of legitimately large archives
- Zip Bomb Protection now only checks compression ratio (>100x), not total size
- Simplified UI descriptions for better user experience

### Added
- **Automatic Error Logging**: Creates detailed error log files (`unpackr-errors-[timestamp].log`) in input directory when issues occur
- Error logs include timestamp, statistics, and full error descriptions

### Improved
- Better error handling flow
- More informative error messages
- Logs are created for both partial failures and critical errors

### Technical
- Added `writeErrorLog()` function for comprehensive error tracking
- Cleaned up unused code from removed size limit checks
- Fixed React types conflict (v18 vs v19)
- All TypeScript and ESLint checks passing

---

## Upgrade Notes

### From 1.3.0 to 1.4.0
- Zip bomb protection now only checks compression ratio, not total archive size
- Error logs will now be automatically created in your input folder if any issues occur
- No breaking changes to configuration or usage

---

## Future Roadmap

### Planned Features
- Batch processing history and statistics
- Support for other archive formats (RAR, 7z)
- Advanced filtering options (by date, size, type)
- Progress persistence across crashes
- Archive integrity verification

---

**Legend:**
- **Added**: New features
- **Changed**: Changes in existing functionality
- **Deprecated**: Soon-to-be removed features
- **Removed**: Removed features
- **Fixed**: Bug fixes
- **Security**: Security improvements
