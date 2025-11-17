# Unpackr

A Raycast extension that automates the process of organizing and merging ZIP files. Originally designed for Google Takeout archives, it now works with any ZIP files.

## Problem

When downloading a Google Photos library via Google Takeout, the service splits the library into multiple .zip files (e.g., `takeout-20250101.zip`, `takeout-20250102.zip`, etc.). When unzipped, these create overlapping and messy directory structures like:
- `Takeout/`
- `Takeout (1)/`
- `Takeout (2)/`

This makes it impossible to merge the photo library easily without manual work.

**But Unpackr isn't just for Google Takeout!** It works with any ZIP files, making it perfect for organizing photo collections from multiple sources, backups, or any batch of ZIP files you need to merge.

## Solution

Unpackr provides a single Raycast command that:
1. Finds all ZIP files in a specified input folder (matching your filter pattern)
2. Unzips all files into a temporary staging directory
3. Intelligently merges the contents into a single output folder
4. Automatically detects Google Takeout structure and organizes accordingly
5. Performs de-duplication by comparing file hashes (SHA256)
6. Renames files with conflicting names but different content
7. Optionally deletes the original ZIP files after successful merge

## How It Works

Unpackr automatically detects the structure of your ZIP files:

**Google Takeout Archives:**
- Detects "Google Photos" folder structure
- Merges to: `[Output Folder]/Google Photos/[your files]`
- Perfect for combining multiple Takeout downloads

**Regular ZIP Files:**
- Merges all files directly to: `[Output Folder]/[your files]`
- Preserves the internal folder structure from the ZIPs
- Great for photo collections, document archives, or any batch of ZIPs

In both cases, duplicate files are automatically detected and skipped!

## Features

- **Universal ZIP Support**: Works with Google Takeout or any ZIP files
- **Intelligent Deduplication**: Uses SHA256 hashes to detect true duplicates
- **Conflict Resolution**: Automatically renames files with same name but different content
- **Progress Tracking**: Real-time toast notifications showing progress
- **Error Recovery**: Continues processing even if individual files fail
- **Safe Defaults**: Preserves original files unless explicitly requested to delete
- **Path Security**: Validates paths and prevents directory traversal attacks

## Installation

1. Clone this repository
2. Run `npm install`
3. Run `npm run dev` to start development
4. The extension will appear in Raycast

## Usage

1. Open Raycast and search for "Merge Google Takeout Files"
2. Select your input folder (containing the ZIP files)
3. Select your output folder (where the merged files should go)
4. Adjust the ZIP name filter:
   - Leave as "takeout-" for Google Takeout files
   - Change to match your ZIP files (e.g., "photos", "backup", or leave blank for all ZIPs)
5. Optionally enable deletion of original ZIP files
6. Click "Start Merging" and wait for the process to complete

### Examples

**Merging Google Takeout archives:**
- Input: `/Users/you/Downloads` (containing `takeout-20250101.zip`, `takeout-20250102.zip`)
- Output: `/Users/you/Pictures`
- Filter: `takeout-`
- Result: `/Users/you/Pictures/Google Photos/[all your photos]`

**Merging regular photo ZIPs:**
- Input: `/Users/you/Downloads` (containing `vacation-1.zip`, `vacation-2.zip`)
- Output: `/Users/you/Pictures/Vacation2025`
- Filter: `vacation`
- Result: `/Users/you/Pictures/Vacation2025/[all your photos]`

## Development

```bash
# Install dependencies
npm install

# Development mode
npm run dev

# Build extension
npm run build

# Lint code
npm run lint

# Fix linting issues
npm run fix-lint
```

## Configuration

You can set default directories in Raycast preferences:
- **Default Input Folder**: Where you typically download Takeout ZIPs (e.g., ~/Downloads)
- **Default Output Folder**: Where your merged library should go (e.g., ~/Pictures)

## Edge Cases Handled

- Empty ZIP files
- Corrupted ZIP files
- Permission errors
- Cross-device file moves
- Path traversal attacks in ZIP files
- Nested input/output directories
- Special characters in filenames
- Files without extensions
- Partial extraction failures
- Insufficient disk space
- Missing Google Photos directories (falls back to regular merge)
- Mixed ZIP types (Google Takeout + regular ZIPs)
- Single or multiple ZIP files
- Any internal folder structure

## Technical Details

- **Language**: TypeScript
- **Platform**: Raycast Extension
- **UI Framework**: React with @raycast/api
- **ZIP Extraction**: yauzl (robust Node.js ZIP library)
- **File Operations**: Node.js fs.promises API
- **Hashing**: crypto SHA256

## Architecture

See [CLAUDE.md](./CLAUDE.md) for detailed architecture documentation.

## License

MIT
