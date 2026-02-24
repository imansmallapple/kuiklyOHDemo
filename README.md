# Kuikly HarmonyOS Demo

This project is a template/demo application for HarmonyOS (OpenHarmony) utilizing the **Kuikly Render** framework for dynamic UI rendering.

## Project Overview

Kuikly is a high-performance, cross-platform dynamic rendering engine. This demo showcases how to integrate `@kuikly-open/render` into a HarmonyOS ArkTS application, including custom view registration and bridge module implementation.

## Key Features

- **Dynamic Rendering**: Host dynamic pages using the `Kuikly` component.
- **Custom Views**: Extend the rendering engine with native ArkTS components (e.g., `KRMyView`).
- **Bridge Modules**: Communication between the rendering engine and native HarmonyOS APIs via `KRBridgeModule`.
- **Native C++ Support**: Integrated NAPI for high-performance native logic.

## Project Structure

```text
├── AppScope/               # Global resources and app configuration
├── entry/                  # Main HAP module
│   ├── src/main/cpp/       # Native C++ source code (NAPI)
│   ├── src/main/ets/       # ArkTS source code
│   │   ├── entryability/   # Ability life cycle management
│   │   ├── kuikly/         # Kuikly framework integration
│   │   │   ├── components/ # Custom Kuikly views (Native ArkUI)
│   │   │   ├── modules/    # Custom Kuikly modules (Bridge)
│   │   │   └── adapter/    # Platform adapters (Log, Router)
│   │   └── pages/          # App entry pages
│   └── src/main/resources/ # Module-specific resources
├── hvigor/                 # Hvigor build tool configuration
└── build-profile.json5     # Build configuration
```

## Prerequisites

- **DevEco Studio**: Latest version recommended.
- **HarmonyOS SDK**: Standard SDK for ArkTS development.
- **Node.js**: Required for OHPM and Hvigor.

## Getting Started

1. **Install Dependencies**:
   Open a terminal in the project root and run:
   ```bash
   ohpm install
   ```

2. **Configure Signing**:
   Before running on a real device or emulator, ensure you have configured the signing information in `build-profile.json5` or via DevEco Studio (Project Structure > Project > Signing Configs).

3. **Build and Run**:
   - Use DevEco Studio to build and run the `entry` module.
   - Or use the provided script (macOS/Linux):
     ```bash
     chmod +x runOhosApp.sh
     ./runOhosApp.sh
     ```

## Usage

### Registering Custom Components
Custom views and modules are registered in `KuiklyViewDelegate.ets`:

```typescript
export class KuiklyViewDelegate extends IKuiklyViewDelegate {
  getCustomRenderViewCreatorRegisterMap(): Map<string, KRRenderViewExportCreator> {
    const map = new Map();
    map.set(KRMyView.VIEW_NAME, () => new KRMyView());
    return map;
  }
  // ...
}
```

### Implementing Bridge Methods
The `KRBridgeModule` allows the rendering engine to call native functions. You can add your own methods in `entry/src/main/ets/kuikly/modules/KRBridgeModule.ets`.

## License

This project is licensed under the [MIT License](LICENSE).
