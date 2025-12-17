# VS Code Workspace Settings

Bu folder workspace-specific settingslarni saqlaydi.

## Settings Priority

VS Code settingslar quyidagi tartibda qo'llaniladi (pastdan yuqoriga prioritet):

1. **Default Settings** - VS Code default sozlamalari
2. **User Settings** - Sizning shaxsiy settings (GitHub Sync orqali keladi)
3. **Workspace Settings** - Bu workspace uchun maxsus settings ✅ (ENG YUQORI PRIORITET)

## Workspace vs Synced Settings

### ✅ Workspace Settings (bu repositoryda)
- `settings.json` - Spark environment uchun zarur sozlamalar
- `launch.json` - Debug configurations
- `extensions.json` - Tavsiya etiladigan extensionlar

Bu settingslar **har doim** sizning synced settingslardan ustun turadi!

### 🔄 GitHub Settings Sync (sizning shaxsiy settingslaringiz)
GitHub Sync orqali quyidagilar sinxronlanadi:
- Color theme preferences
- Keyboard shortcuts
- UI preferences
- Other extensions
- Personal editor settings

**MUHIM:** Workspace settings (bu folder) har doim prioritetga ega!

## Nima ishlatiladi?

```
Python Interpreter: /usr/local/bin/python (workspace)
SPARK_HOME: /opt/spark (workspace)
Icon Theme: material-icon-theme (workspace)
Color Theme: [sizning synced settingingiz] ✅
Keyboard Shortcuts: [sizning synced settingingiz] ✅
Editor Font: [sizning synced settingingiz] ✅
```

Demak, GitHub Sync ishlay veradi, faqat Spark-specific sozlamalar workspace dan olinadi! 🎉
