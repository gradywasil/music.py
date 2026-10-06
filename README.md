# music.py

**An experimental Python script for reorganizing music folders by filename.**

This is unfinished filesystem-tooling work. The current script immediately moves folders and renames files, with no dry run, backup, confirmation, or undo. **Do not use it on an original or irreplaceable music library.** Any experimentation should use disposable copies in a separate test directory.

## Intended transformation

The script attempts to convert this naming convention:

```text
Artist - Album/
└── Artist - Album - Track Title.mp3
```

into this structure:

```text
Artist/
└── Album/
    └── Track Title.mp3
```

This is an illustration of the intended behavior, not evidence of a successful run. The script reads names, not audio tags or metadata.

## Expected inputs

| Input | Expected naming |
| --- | --- |
| Album folder | Exactly two parts separated by ` - ` |
| Track filename | Exactly three parts separated by ` - ` |
| Recognized audio extensions | Lowercase `.mp3` and `.flac` |
| Starting location | The process's current working directory |

It does not convert audio, edit ID3 tags, fetch album art, play music, or provide a graphical interface. Other formats and uppercase extensions are not handled by its audio-file branch.

## Implementation

The project uses Python's standard-library `os` and `shutil` modules. There are no third-party requirements or command-line options. The entry point starts traversal from `os.getcwd()` and performs filesystem operations using relative paths.

| File | Role |
| --- | --- |
| `music.py` | Directory traversal, album-folder moves, and track renaming |
| `test_music.py` | Empty test source; not an implemented test suite |

No supported Python version is declared. This documentation pass reviewed the source without running filesystem mutations.

## Known limitations

- Traversal receives a root path, but the operations use bare directory names. Nested paths may therefore be handled incorrectly.
- The script changes the working directory and does not restore it, which can affect later relative-path operations.
- Unexpected delimiters or filenames can interrupt the run after earlier changes have already happened.
- Destination collisions and partial failures have no deliberate recovery mechanism.
- Matching folder names are not sufficient to establish that a directory is actually a music album.

Before considering real-library use, the implementation needs explicit target-path handling, a dry-run plan, collision checks, repeatable fixture tests, and a recoverable execution strategy. Those protections are not present in this version.

## Project background

An experimental personal utility by [Grady Wasil](https://github.com/gradywasil), developed in late 2023 while exploring Python filesystem operations. It is preserved here as learning work, rather than presented as a tested file-management release.
