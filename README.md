# GeoLens (空间几何对象可视化与投影转换工具)

- [简体中文](#简体中文)
- [English](#english)

---

## 简体中文

这是一个基于单文件 HTML5 的轻量、功能强大的空间几何对象可视化与投影转换工具。通过直观的 Web 界面，您可以在地图上轻松解析、编辑、投影并导出各种空间向量几何数据。

### 🌟 核心功能

#### 1. 多格式自动检测与解析
支持以下主流空间地理数据格式的自动检测、解析与底图渲染：
- **WKT (Well-known Text)**: 标准点 (Point)、线 (LineString)、面 (Polygon)、多面 (MultiPolygon)、几何集合 (GeometryCollection) 等，如 `POINT(-74.006 40.7128)`。
- **EWKT**: 包含空间参考标识符 (SRID) 的扩展 WKT，如 `SRID=4326;POINT(-74.006 40.7128)`。
- **Hex WKB (Well-known Binary)**: 十六进制表示的二进制空间数据。
- **Hex EWKB**: 包含 SRID 的扩展十六进制 WKB 数据。
- **GeoJSON**: 支持解析 `Geometry`、`Feature` 和 `FeatureCollection` 结构。
- **Geohash**: 地理哈希编码，如 `dr5reg`。
- **Uber H3 Index**: 优步 H3 六边形网格索引，如 `852a1077fffffff`。

#### 2. 交互式地图与手绘工具
- **多底图切换**: 内置五种精美底图，包括 CartoDB 极简深色、CartoDB 极简浅色、标准 OpenStreetMap、等高地形图 (OpenTopoMap) 以及 Esri 卫星影像图。
- **Leaflet Geoman 手绘面板**: 支持在地图上直接绘制点、圆点、折线、多边形、矩形和圆形。
- **编辑与拖拽**: 支持对已有几何图层进行二次节点编辑、整体拖拽和删除。
- **实时坐标显示**: 鼠标滑动时实时显示当前位置在所选坐标系（如投影坐标下的米，或地理坐标下的经纬度）中的坐标。

#### 3. 多坐标系支持与投影转换 (CRS)
- **内置常用坐标系**: 预置 EPSG:4326 (WGS 84), EPSG:3857 (Web Mercator), EPSG:4269, EPSG:27700 (OSGB36), EPSG:3035 以及常用 UTM 分带（32631 - 32633）。
- **动态 CRS 查找**: 支持输入任意 4-5 位 EPSG 代码，一键从 `epsg.io` 动态拉取 Proj4 定义并注册。
- **Proj4 定义在线编辑**: 用户可手动输入或修改 Proj4 参数，以支持自定义或非标准坐标系。

#### 4. 几何导出与复制
- 支持在下拉菜单中一键将地图上绘制的所有几何体打包转换为：
  - **WKT**: 标准文本格式。
  - **WKB**: 十六进制二进制格式。
  - **EWKB**: 带 SRID 的十六进制格式。
  - **GeoJSON**: 标准 JSON 地理格式。
  - **Bounding Box (BBOX)**: 包含当前所有几何范围的 `minX, minY, maxX, maxY` 矩形边界框。

#### 5. 导入文件
- 支持将外部 `.wkt`, `.geojson`, `.json`, `.wkb`, `.txt` 文件直接导入到编辑器中进行可视化。

#### 6. 高级主题与自适应
- **自适应暗色/亮色模式**: 首次加载时根据系统原生偏好自动设置，并提供一键手动切换。
- **优雅的玻璃拟态 UI**: 采用 Outfit & JetBrains Mono 现代字体，拥有毛玻璃效果的控制面板和流畅的微动画。
- **自动状态持久化**: 使用 `localStorage` 自动保存当前编辑器文本、选择的 EPSG 代码和 Proj4 定义，防止刷新后丢失工作进度。

### ⌨️ 全局快捷键

在非输入状态下，可使用以下快捷键：
- **`Delete` / `Backspace`**: 快速删除当前处于选中状态的几何图层。
- **`Escape`**: 退出当前的手绘工具绘制模式。

### 🛠 运行与使用

该项目采用**单 HTML 文件架构**，所有的样式、脚本和依赖都整合在 [index.html](file:///c:/projects/wkb/index.html) 中，无需任何编译、打包或安装步骤。

#### 方式一：直接双击打开
您可以通过文件管理器直接双击运行：
`c:\projects\wkb\index.html`

#### 方式二：通过本地服务器运行（推荐）
为了获得最佳的静态资源加载体验（避免部分浏览器的跨域请求限制），推荐使用任意轻量级 HTTP 服务器启动：

**使用 Python 启动：**
```bash
# 进入项目所在目录
cd c:\projects\wkb
# 启动内置服务器
python -m http.server 8000
```
然后通过浏览器访问 `http://localhost:8000/`。

**使用 Node.js 启动：**
```bash
npx serve
```

### 📦 第三方依赖库

该项目所有依赖均通过可靠的 CDN 异步加载，您无需在本地保存依赖库：
- [Leaflet (v1.9.4)](https://leafletjs.com/) - 核心地图渲染框架。
- [Leaflet Geoman (v2.17.0)](https://geoman.io/) - 地图图形手绘与编辑插件。
- [Proj4js (v2.11.0)](https://github.com/proj4js/proj4js) - 用于客户端坐标变换。
- [wellknown (v0.5.0)](https://github.com/mapbox/wellknown) - WKT 与 GeoJSON 相互转换。
- [wkx (v0.5.0)](https://github.com/cschwarz/wkx) - WKB/EWKB 二进制与 GeoJSON 相互转换。
- [buffer (v6.0.3)](https://github.com/feross/buffer) - 浏览器端的二进制处理 Polyfill。
- [h3-js (v4.1.0)](https://github.com/uber/h3-js) - 优步 H3 六边形网格层解析库。

---

## English

A lightweight, powerful, single-file HTML5-based web application for parsing, visualizing, editing, reprojecting, and exporting vector geometries. With an intuitive interface, you can easily work with spatial data directly in your browser.

### 🌟 Core Features

#### 1. Format Auto-Detection & Parsing
Automatically detects and renders the following geospatial vector data formats:
- **WKT (Well-known Text)**: Standard geometries such as `POINT`, `LINESTRING`, `POLYGON`, `MULTIPOLYGON`, and `GeometryCollection` (e.g., `POINT(-74.006 40.7128)`).
- **EWKT (Extended WKT)**: Well-known Text containing SRID prefixes (e.g., `SRID=4326;POINT(-74.006 40.7128)`).
- **Hex WKB (Well-known Binary)**: Hexadecimal representation of binary spatial geometry.
- **Hex EWKB (Extended WKB)**: Hexadecimal WKB containing SRID headers.
- **GeoJSON**: Supports parsing standard GeoJSON `Geometry`, `Feature`, and `FeatureCollection` structures.
- **Geohash**: Geohash coordinates (e.g., `dr5reg`).
- **Uber H3 Index**: Uber's hexagonal hierarchical spatial index (e.g., `852a1077fffffff`).

#### 2. Interactive Map & Drawing Tools
- **Basemap Switcher**: Toggle between five beautiful basemaps, including CartoDB Dark Matter, CartoDB Positron, standard OpenStreetMap, OpenTopoMap, and Esri World Imagery.
- **Leaflet Geoman Controls**: Draw points, circle markers, polylines, rectangles, polygons, and circles directly on the map.
- **Edit & Drag**: Interactively edit vertices, drag layers, or remove geometries from the map.
- **Live Cursor Tracking**: Real-time display of cursor coordinates projected in the active Coordinate Reference System (meters, degrees, etc.).

#### 3. Coordinate Projections & CRS Support
- **Built-in Projections**: Pre-configured common systems: EPSG:4326 (WGS 84), EPSG:3857 (Web Mercator), EPSG:4269, EPSG:27700 (OSGB36), EPSG:3035, and common UTM zones (32631 - 32633).
- **Dynamic CRS Resolution**: Input any 4-5 digit EPSG code to dynamically fetch Proj4 definitions from `epsg.io` and register them instantly.
- **Custom Proj4 Editing**: Edit Proj4 parameters manually to support custom, local, or non-standard reference systems.

#### 4. Export & Copy Geometries
- Export all drawn geometries via the Copy dropdown into:
  - **WKT**: Standard Well-known Text.
  - **WKB**: Hexadecimal Well-known Binary.
  - **EWKB**: Hexadecimal EWKB with current SRID.
  - **GeoJSON**: Standard GeoJSON representation.
  - **Bounding Box (BBOX)**: Bounding box limits (`minX, minY, maxX, maxY`) projected in the active CRS.

#### 5. File Import
- Import files containing `.wkt`, `.geojson`, `.json`, `.wkb`, or `.txt` directly into the editor for instant visualization.

#### 6. Aesthetics & Theme Sync
- **System Theme Auto-Detection**: Synchronizes with OS light/dark mode preference on initial load, with a manual toggle button.
- **Modern Glassmorphism UI**: Beautifully styled sidebar using `Outfit` & `JetBrains Mono` fonts, featuring backdrop blurs and subtle micro-animations.
- **State Persistence**: Auto-saves editor content, EPSG code, and Proj4 parameters to `localStorage` to preserve progress across refreshes.

### ⌨️ Global Keyboard Shortcuts

When not typing in inputs/textareas:
- **`Delete` / `Backspace`**: Quickly remove selected layers from the map.
- **`Escape`**: Cancel the current drawing mode.

### 🛠 Getting Started

The project is built on a **single HTML file architecture**. All styling, scripts, and dependencies are packed inside [index.html](file:///c:/projects/wkb/index.html). No build, compile, or install steps are required.

#### Method 1: Open Directly
Double-click and open the file in any browser:
`c:\projects\wkb\index.html`

#### Method 2: Serve Locally (Recommended)
To prevent potential CORS issues with browser file restrictions, serve the folder using any HTTP server:

**Using Python:**
```bash
cd c:\projects\wkb
python -m http.server 8000
```
Then navigate to `http://localhost:8000/`.

**Using Node.js:**
```bash
npx serve
```

### 📦 Dependencies

All external libraries are loaded asynchronously via CDN. No local installations required:
- [Leaflet (v1.9.4)](https://leafletjs.com/) - Map rendering engine.
- [Leaflet Geoman (v2.17.0)](https://geoman.io/) - Map drawing & editing.
- [Proj4js (v2.11.0)](https://github.com/proj4js/proj4js) - Coordinate transformations.
- [wellknown (v0.5.0)](https://github.com/mapbox/wellknown) - WKT parsing.
- [wkx (v0.5.0)](https://github.com/cschwarz/wkx) - WKB/EWKB binary parsing.
- [buffer (v6.0.3)](https://github.com/feross/buffer) - Buffer polyfill.
- [h3-js (v4.1.0)](https://github.com/uber/h3-js) - Uber H3 index boundaries.
