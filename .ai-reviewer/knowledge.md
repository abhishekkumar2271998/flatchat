# flatchat reviewer notes

## Architecture
The `flatchat` repository comprises an Electron application that leverages a Python backend for audio recording, transcription, and summarization. The project is structured with a clear separation between the frontend (`app/` for the Electron interface using React and TypeScript) and the backend (`src/` for the Python components), facilitating modular development.

## Conventions
- **Python Code Style**: Adheres to PEP 8 guidelines as specified in `CONTRIBUTING.md`. All functions and classes should include docstrings for clarity (e.g., `audio_recorder.py`, `transcriber.py`).
- **JavaScript/TypeScript Code**: Uses `const` and `let` for variable declarations and requires the use of semicolons (as per `CONTRIBUTING.md`). The project employs `Prettier` for formatting and `ESLint` for static code analysis, ensuring consistency and preventing errors.
- **Branch Naming**: Feature branches follow the convention `feature/<feature-name>` (see `CONTRIBUTING.md`).
- **Directory Structure**:
  - `app/`: Contains the Electron-related files, including `main.js` for the main process and `renderer/` for the React application.
  - `src/`: Houses the backend Python scripts responsible for key functionalities like audio recording and AI integrations.
  - `simple_recorder.py`: Serves as the command-line interface for user interaction with the backend.

## Intentional non-standard choices
- **Custom Environment Loading**: The custom `.env` loading mechanism in `main.js` is minimalistic, designed to load environment variables without overwriting existing ones. This approach is intentional to ensure flexibility during both development and production stages. 

## Watch out for
- **Javascript/TypeScript Linting**: Ensure that `ESLint` is configured correctly and that the code adheres to the defined rules, particularly within the `renderer` directory files like `App.tsx` and `index.html`.
- **Inter-Process Communication (IPC)**: Be cautious of the IPC contracts between the `main` and `renderer` processes. Any mismatches in expected channels could lead to runtime issues. Check implementations in `preload.js` to ensure proper channel exposure and handling.
- **Python Testing**: Acknowledgment that Python testing commands are present should be mandatory before merging, especially after changes in `src/`. Review commits that modify functionality related to audio processing, transcription, or summarization in `transcriber.py` and `audio_recorder.py`.
- **Electron Build Management**: Ensure that `electron-builder` configurations are optimized to reduce the package size and avoid including unnecessary source maps in production builds (`vite.config.ts`). Also, verify that the app correctly handles macOS permissions for microphone and screen recording.

In conclusion, this playbook establishes foundational guidelines for maintaining the `flatchat` repository within the architectural and coding conventions the team has embraced, while highlighting potential pitfalls to ensure a smooth development process.