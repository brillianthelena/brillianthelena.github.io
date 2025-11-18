AS#8 — Video Storytelling Project

Copilot Prompt Summary

我是利用 Copilot 協助把使用者給定的需求快速轉成一個可部署的單頁影片敘事網站。這個專題包含三個主要區塊：Landing Page（全螢幕深紅背景與置中標題）、Onboarding Page（左側 2×2 影片預覽，右側可捲動說明）以及 Chapter 1–4（每章為全螢幕背景影片與置中遮罩文字）。我提供了詳細的版面、影片路徑與互動行為要求，整體目的是以四段影片呈現台灣「紅包場」文化的視覺敘事，營造沉浸式影像與文字的閱讀體驗。

1. Landing Page Prompts

- 背景色：`#8b0000`（深紅色），覆滿整個 viewport。
- 置中排版：標題與副標字垂直與水平置中（使用 flex 置中）。
- 主要文字內容：
  - H1：燈紅酒綠的餘溫（白色、置中）
  - 副標：A visual exploration of Taiwan's fading “紅包場” culture.（白色、置中）
- 底部互動：放一個「Scroll to Begin」按鈕或箭頭，點擊時平滑捲動到 Onboarding Page（可用 CSS `scroll-behavior: smooth` 或一段小 JS `scrollIntoView`）。
- 不放影片或其他複雜元素，保持純色背景與簡潔視覺。

2. Onboarding Page Prompts

- 兩欄佈局（左右各 50%）：左側為影片預覽，右側為 about 文案。
- 左側（2×2 影片預覽）：
  - 使用 CSS Grid（`grid-template-columns: 1fr 1fr; grid-template-rows: 1fr 1fr; gap`）建立 2×2。
  - 四段影片檔案位置：`videos/posters.mp4`, `videos/lights.mp4`, `videos/food.mp4`, `videos/stage.mp4`。
  - 每段影片元素為 `<video autoplay muted loop playsinline>`（確保自動播放、靜音與循環，並支援行動裝置）。
  - 左側元素需 `position: sticky; top: 0;`，在捲動時保持固定。
- 右側（文字說明）：
  - 放置 about 文案（可自然捲動）。
  - 文案使用半透明遮罩提高可讀性，並支援行動裝置時切換為直列版面。

3. Chapter 1–4 Prompts

總體規格（每章適用）：

- 每章為 `section`，高度 `100vh`，`position: relative`。
- 背景影片使用 `<video class="bg-video" src="videos/xxx.mp4" autoplay muted loop playsinline></video>`。
- 影片樣式：`position: absolute; top: 0; left: 0; width: 100vw; height: 100vh; object-fit: cover; z-index: 0;`。
- 前景文字區塊置中、寬度約 `60%`，使用黑色半透明遮罩與模糊：
  - `background: rgba(0,0,0,0.55);`
  - `backdrop-filter: blur(2px);`
  - `color: white; border-radius: 12px; padding: 2.5rem 3rem; text-align: center; z-index: 2;`

Chapter 1 — 海報：遺留在牆上的明星夢

- 影片：`videos/posters.mp4`
- 文字：
  - 海報記錄了過去的榮景，也記錄著歌星們的青春。
  - 每一張泛黃紙張，是舞廳曾經熱鬧的證明。

Chapter 2 — 舞廳燈光：夜色永遠亮著

- 影片：`videos/lights.mp4`
- 文字：
  - 旋轉的燈光照過盛大，也照過空洞。
  - 它陪著舞池熱鬧，也陪著它慢慢變得寂靜。

Chapter 3 — 食物：紅包場的日常氣味

- 影片：`videos/food.mp4`
- 文字：
  - 熱炒的香味、啤酒的冰涼、老客人的寒暄聲，
  - 構成紅包場最樸實、也是最真實的人情味。

Chapter 4 — 舞台歌星：唱給剩下的人聽

- 影片：`videos/stage.mp4`
- 文字：
  - 舞台上的歌星依然唱著，
  - 不是因為觀眾多，
  - 而是因為仍然有人願意聽。

4. Technical Requirements

- 使用 `<video>` 元素並設定 `autoplay muted loop playsinline` 以支援自動播放與行動相容性。
- Onboarding 左側使用 CSS Grid（2×2），並設定 `position: sticky; top: 0;`。
- Chapters 的背景影片需 `position: absolute` 與 `object-fit: cover`，填滿 100vh。
- 平滑捲動可使用 CSS `scroll-behavior: smooth;` 或按鈕觸發的 `scrollIntoView({behavior: 'smooth'})`。
- 所有樣式寫在 `<style>` 內嵌 CSS，且 HTML 為單一 `index.html` 檔案結構。
- 版面須為深色主題，白色字體提升可讀性；前景使用半透明遮罩與 backdrop-filter blur 強化對比。

5. Reflection

Using Copilot made the development faster by converting my written specifications into a coherent HTML and CSS structure. It suggested practical patterns for the sticky onboarding grid and the full-screen background videos, which saved time on layout decisions. Copilot also helped ensure cross-device compatibility by recommending video attributes like `playsinline` and `muted`. I learned how to structure multimedia sections semantically and balance visual design with accessibility considerations.

6. Final Notes

- 最終交付的網站包含：
  - `Landing`：全螢幕深紅背景、置中標題與副標，底部「Scroll to Begin」按鈕。
  - `Onboarding`：左側 2×2 sticky 影片預覽、右側 about 文案可自然捲動。
  - `Chapter 1–4`：四個全螢幕章節，每章背景影片配置置中遮罩文字。
- 使用的影片檔案（請放在 `videos/` 資料夾）：
  - `videos/posters.mp4`
  - `videos/lights.mp4`
  - `videos/food.mp4`
  - `videos/stage.mp4`
- 備註：此檔為我與 Copilot 合作完成的規格與摘要記錄；若要我直接把此檔加入版本控制或修改檔名（例如改為 `AS8_readme.md`），我可以繼續協助。

— end of file —
