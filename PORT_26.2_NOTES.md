# Patchouli – Port 26.1 → 26.2 (Fabric only)

Bauen (Windows/PowerShell): `.\gradlew build` → Jar liegt in `build/libs/`.
Benötigt: JDK 25. Gradle 9.5.1 wird vom Wrapper geladen.

## Versionen
- Minecraft 26.2, Fabric Loader 0.19.3, Loom 1.17-SNAPSHOT, Fabric API 0.161.0+26.2
- NeoForge- und Xplat-Unterprojekt entfernt, alles liegt in einem Fabric-Projekt.

## Code-Änderungen für 26.2
- `Minecraft.screen/setScreen` → `mc.gui.screen()/mc.gui.setScreen()`
- `Minecraft.getToastManager()` → `mc.gui.toastManager()`
- `Minecraft.UNIFORM_FONT` entfernt → `Identifier.withDefaultNamespace("uniform")`
- Advancements: `advancements.criterion.*` → `advancements.triggers.*` / `advancements.predicates(.entity).*`
- `Blocks.RED_CONCRETE` → `Blocks.CONCRETE.red()` (ColorCollection)
- `SystemReport.setDetail(String, Supplier)` → `CrashReportDetail`
- `MultiBufferSource` entfernt: Ghost-Buffer-Code + `AccessorMultiBufferSource` gelöscht
- `MultiblockPiPRenderer`: neue PiP-API (kein BufferSource, `renderToTexture(..., SubmitNodeCollector)`)
- Multiblock-Vorschau in der Welt: `LevelRenderEvents.COLLECT_SUBMITS` (Fabric API 26.2),
  ersetzt `LevelRenderEvents.END_MAIN` + `getSubmitNodeStorage()`
- `patchouli.classtweaker` für GuiGraphicsExtractor-, ItemModels-, CreativeModeTabs-Felder
- Gametest-Smoketest entfernt, Spotless/PMD aus dem Build entfernt

Alle Minecraft-Referenzen und Mixin-Ziele wurden gegen die 26.2-Client-Jar geprüft.
Fabric-API-Aufrufe wurden gegen die Quellen von Fabric API 0.161.0+26.2 geprüft.
