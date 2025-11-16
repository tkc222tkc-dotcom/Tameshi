# Game Center Application

## Overview

This is a Japanese-language game center web application featuring a collection of classic board and puzzle games. The application provides single-player experiences with AI opponents of varying difficulty levels. Games include:

- **Othello (オセロ)** - Classic reversi game with AI opponent
- **Tic-Tac-Toe (まるばつゲーム)** - Three-in-a-row game with AI
- **Shogi (将棋)** - Japanese chess with piece promotion and captured piece mechanics
- **Chess (チェス)** - International chess with AI opponent
- **Tetris (テトリス)** - Classic falling blocks puzzle game
- **Memory (神経衰弱)** - Card matching memory game

The application serves as a portfolio of game implementations with client-side game logic and AI algorithms.

## Recent Changes

### 2025年11月15日 - バグ修正とゲーム追加

**バグ修正**:
1. **オセロ**: ゲーム終了判定を追加。両プレイヤーが移動できなくなった時に自動的に勝敗を判定し、スコアを表示。相手のコマの上に置けないようにチェック機能を追加。
2. **チェス**: コマの色を視覚的に区別できるようCSS追加。白いコマは明るい色（#f0f0f0）、黒いコマは暗い色（#1a1a1a）で表示され、text-shadowで視認性を向上。
3. **テトリス**: restart()関数でDOMノードがリークする問題を修正。init()関数でboardEl.innerHTML = ''を追加してセルを再作成前にクリア。

**新規ゲーム追加**:
1. **テトリス**: 完全に機能するテトリスゲームを実装。スコア、レベル、ライン数の追跡機能付き。キーボード操作（矢印キー、スペースキー）に対応。
2. **神経衰弱**: 8ペアのカードマッチングゲームを実装。手数、ペア数、時間の追跡機能付き。カードのフリップアニメーション付き。

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Technology Stack**: Pure HTML5, CSS3, and vanilla JavaScript with no external frameworks or libraries.

**Rationale**: This architecture provides maximum simplicity and portability. Games run entirely in the browser with no build step required. The choice eliminates dependency management overhead and ensures games load instantly with minimal bandwidth.

**Structure**: Each game is a standalone HTML file containing embedded CSS and JavaScript. This self-contained approach means:
- No asset loading delays
- Easy to maintain individual games independently  
- Simple deployment (just copy files)
- No bundling or compilation required

**UI Design Pattern**: CSS Grid-based layouts for game boards with consistent dark theme (#222 background) across all games. Visual feedback through CSS transitions, hover states, and class-based state management (e.g., `.selected`, `.legal-move`, `.flipped`).

**Game State Management**: Client-side state maintained in JavaScript closures and global variables within each HTML file. No state persistence across sessions - games reset on page reload.

### Backend Architecture

**Server Implementation**: Minimal Node.js HTTP server (`server.js`) serving static files.

**Purpose**: The server exists solely to serve HTML files with proper MIME types and cache headers. It implements:
- Static file serving with automatic `index.html` routing
- MIME type detection for `.html`, `.js`, and `.css` files
- Cache-Control headers set to prevent caching during development
- 404 and 500 error handling

**Rationale**: A lightweight custom server was chosen over frameworks like Express to minimize dependencies. The application has no backend logic, database, or API requirements - it simply needs to deliver static files to browsers.

**Port Configuration**: Listens on port 5000 with binding to `0.0.0.0` for accessibility in containerized environments (like Replit).

### Game Logic Architecture

**AI Implementation**: Each board game implements its own AI opponent using minimax or similar game tree search algorithms with varying depths to control difficulty.

**Board Representation**: Games use 2D array structures to represent board states, with CSS Grid rendering synchronized to the underlying data model.

**Move Validation**: Client-side rule engines validate legal moves before applying state changes. Visual indicators (CSS classes) highlight valid move targets.

**Event Handling**: Click event listeners on game board cells trigger move validation, state updates, AI responses, and UI re-rendering in sequence.

## External Dependencies

### Runtime Dependencies

**Node.js Core Modules**:
- `http` - HTTP server functionality
- `fs` - File system operations for reading static files
- `path` - Path manipulation for file routing

**Browser APIs**:
- DOM manipulation APIs
- CSS Grid and Flexbox layout engines
- Event handling system
- No external JavaScript libraries

### Development Environment

**Server Runtime**: Node.js environment (no specific version constraints in repository)

**Hosting Platform**: Designed for Replit deployment based on port configuration and `0.0.0.0` binding

### No External Services

The application is completely self-contained with:
- No database connections
- No external API calls
- No authentication services
- No CDN dependencies
- No analytics or tracking

All game logic, AI algorithms, and UI rendering happen entirely client-side with no external service integrations.