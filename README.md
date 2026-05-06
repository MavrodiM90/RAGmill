RAGmill
Turn any document into clean, chunk-ready Markdown — right in your browser.

No server. No login. No API key. Your files never leave your machine.

🔗 Live demo → mavrodim90.github.io/RAGmill

________________________________________
The problem
You're building a RAG pipeline. Your knowledge base lives in Notion, Obsidian, Confluence, or Jupyter notebooks. You export it — and get a mess of UUIDs, broken links, HTML tags, wiki-style references, and inconsistent formatting that confuses your embeddings and pollutes your vector store.

You fix it by hand. Every. Single. Time.

RAGmill automates that.

________________________________________
What it does
RAGmill is a browser-based document converter that prepares any Markdown-adjacent format for RAG ingestion in three steps:

Raw document → Clean Markdown → Chunks with metadata → Vector DB
Auto-detect sources
Paste or drop your file — RAGmill identifies the source automatically:

Source	What gets cleaned
Notion	UUID tails, broken internal links, empty tables, HTML wrappers
Obsidian	[[wiki links]], frontmatter YAML, ![[embeds]], tags
Confluence	{info}, {code}, {panel} macros → native Markdown
Jupyter	.ipynb JSON → Markdown cells + fenced code blocks
HTML	Full conversion via DOMParser: headings, lists, tables, links, code
Google Docs	Smart quotes, [^footnotes], whitespace normalization
Plain MD	Universal cleanup: invisible chars, CRLF, trailing spaces
Three output modes
Clean — removes noise, preserves structure. Outputs clean .md.

Chunks — splits into pieces with metadata, ready for your vector DB:

-	4 chunking strategies: by headings (with breadcrumb paths), by paragraphs, sliding window with overlap, recursive splitter (à la LangChain)
-	3 output formats: Generic JSON, LangChain Documents, CSV
-	Duplicate detection via Jaccard similarity
-	Oversized chunk warnings

Plain text — strips all Markdown formatting. Pure text for models that choke on syntax.
Result views
-	Raw — the output code, copy or download
-	Preview — rendered Markdown (built-in renderer, no dependencies)
-	Diff — line-by-line diff of what changed, LCS algorithm with context compaction
-	Cards (chunks mode) — chunk cards with path breadcrumbs, expand/collapse, duplicate/oversized flags

________________________________________
Features
-	Auto-detect source type on paste/drop — no manual selection required
-	Drag-and-drop files directly onto the input area (.md, .txt, .html, .ipynb)
-	Presets — one-click configuration for Relevance AI, LangChain, Generic embeddings
-	Share settings — copy a URL with all current settings encoded in query params
-	Persistent settings — everything saved to localStorage between sessions
-	Built-in tests — 22 unit tests for regex and chunking logic, run them in-browser
-	Keyboard shortcuts — Ctrl+Enter reprocess · Ctrl+S download · Ctrl+Shift+C copy
-	Dark mode — follows system preference
-	Mobile-friendly — works on tablets

________________________________________
Privacy
Everything runs locally. When you paste a document or drop a file:

-	It is processed by JavaScript in your browser tab
-	Nothing is sent to any server
-	No analytics, no tracking, no logs
-	Closing the tab clears everything

This matters when your knowledge base contains internal company data, student records, or anything you wouldn't want passing through a third-party API.

________________________________________
Limitations
Without external libraries (by design — zero dependencies), the following are not supported:

-	.zip archives — unpack first, then drop the .md files
-	.docx / .pdf — planned for a future version with optional CDN libs
-	Exact token counting — current estimate: chars / 3.5 (accurate enough for chunking decisions)

________________________________________
Tech
Pure HTML + CSS + JavaScript. One file. No build step. No framework. No npm.

index.html   ~94 KB   zero external dependencies

Open the file locally — it works. Upload to any static host — it works. GitHub Pages — it works.

Algorithms used:

-	LCS (Longest Common Subsequence) for diff
-	Shingle-based Jaccard similarity for duplicate detection
-	Recursive character splitter (same logic as LangChain's RecursiveCharacterTextSplitter)
-	DOMParser API for HTML → Markdown conversion

________________________________________
Roadmap
	ZIP archive support (via JSZip)
	DOCX conversion (via mammoth.js)
	PDF text extraction (via pdf.js)
	Exact token counting (tiktoken WASM)
	Direct export to Pinecone / Weaviate / Chroma
	Batch processing with per-file output

________________________________________
Contributing
Issues and PRs are welcome. If you find a document format that doesn't clean up correctly — open an issue and attach a sanitized sample. The regex patterns are all in index.html and covered by built-in tests.

________________________________________
License
MIT

________________________________________
Author
Built by Alibek Ismailov (@MavrodiM90) — AI Operations & Automation, Petropavl, Kazakhstan.

If RAGmill saved you time, a ⭐ on GitHub is the best way to say so.

________________________________________

________________________________________
RAGmill — русская версия
Превращает любой документ в чистый Markdown, готовый для RAG — прямо в браузере.

Без сервера. Без регистрации. Без API-ключей. Файлы не покидают Ваш компьютер.

🔗 Открыть → mavrodim90.github.io/RAGmill

________________________________________
В чём проблема
Вы строите RAG-пайплайн. База знаний живёт в Notion, Obsidian, Confluence или Jupyter-ноутбуках. Вы экспортируете её — и получаете мешанину из UUID-хвостов, сломанных ссылок, HTML-тегов, вики-ссылок и непоследовательного форматирования.

Всё это засоряет эмбеддинги и снижает качество поиска в векторной БД.

Каждый раз правите руками. RAGmill делает это автоматически.

________________________________________
Что умеет
RAGmill — браузерный конвертер документов, который подготавливает любой MD-смежный формат для загрузки в RAG за три шага:

Сырой документ → Чистый Markdown → Чанки с метаданными → Векторная БД
Автоопределение источника
Вставьте или перетащите файл — RAGmill сам определит тип:

Источник	Что очищается
Notion	UUID-хвосты, сломанные ссылки, пустые таблицы, HTML-обёртки
Obsidian	[[wiki-ссылки]], frontmatter YAML, ![[эмбеды]], теги
Confluence	Макросы {info}, {code}, {panel} → нативный Markdown
Jupyter	.ipynb JSON → MD-ячейки + fenced code блоки
HTML	Полная конвертация через DOMParser: заголовки, списки, таблицы, ссылки, код
Google Docs	Smart quotes, сноски [^1], нормализация пробелов
Plain MD	Универсальная чистка: невидимые символы, CRLF, trailing пробелы
Три режима вывода
Очистить — убирает мусор, сохраняет структуру. Выдаёт чистый .md.

Чанки — разбивает на куски с метаданными, готовые для векторной БД:

-	4 стратегии нарезки: по заголовкам (с breadcrumb-путями), по абзацам, скользящее окно с перекрытием, рекурсивный сплиттер (как LangChain)
-	3 формата вывода: Generic JSON, LangChain Documents, CSV
-	Определение дубликатов через Jaccard similarity
-	Предупреждения о слишком крупных чанках

Plain text — снимает всю разметку. Чистый текст для моделей, которые чувствительны к синтаксису.
Три вида результата
-	Сырой — код результата, скопировать или скачать
-	Превью — отрендеренный Markdown (встроенный рендерер, без зависимостей)
-	Diff — построчное сравнение «было / стало», LCS-алгоритм со сворачиванием контекста
-	Карточки (режим чанков) — карточки с breadcrumb-путями, раскрытием содержимого, пометками дублей и крупных чанков

________________________________________
Возможности
-	Auto-detect — тип источника определяется автоматически при вставке или перетаскивании
-	Drag-and-drop файлов прямо на поле ввода (.md, .txt, .html, .ipynb)
-	Пресеты — одним кликом настройка под Relevance AI, LangChain, Generic embeddings
-	Share-ссылка — копирует URL со всеми текущими настройками в query-параметрах
-	Сохранение настроек — всё сохраняется в localStorage между сессиями
-	Встроенные тесты — 22 unit-теста для регулярок и логики чанкования, запускаются прямо в браузере
-	Хоткеи — Ctrl+Enter переобработать · Ctrl+S скачать · Ctrl+Shift+C скопировать
-	Тёмная тема — следует системным настройкам
-	Мобильная версия — работает на планшетах

________________________________________
Приватность
Всё выполняется локально. Когда Вы вставляете документ или перетаскиваете файл:

-	JavaScript обрабатывает его прямо во вкладке браузера
-	Ничего не отправляется ни на какой сервер
-	Нет аналитики, нет трекинга, нет логов
-	Закрыли вкладку — всё исчезло

Это важно, если Ваша база знаний содержит внутренние данные компании, материалы студентов или любую информацию, которую Вы не хотите передавать через сторонние API.

________________________________________
Ограничения
Без внешних библиотек (zero dependencies — принципиальное решение):

-	.zip-архивы — распакуйте вручную, затем перетащите .md-файлы
-	.docx / .pdf — запланировано в следующей версии с опциональными CDN-библиотеками
-	Точный подсчёт токенов — текущая оценка: символы / 3.5 (достаточно для решений по чанкованию)

________________________________________
Технологии
Чистый HTML + CSS + JavaScript. Один файл. Без сборки. Без фреймворков. Без npm.

index.html   ~94 КБ   ноль внешних зависимостей

Откройте файл локально — работает. Загрузите на любой статический хостинг — работает.

Алгоритмы:

-	LCS (Longest Common Subsequence) для diff
-	Shingle-based Jaccard similarity для определения дубликатов
-	Рекурсивный character splitter (та же логика, что в LangChain RecursiveCharacterTextSplitter)
-	DOMParser API для конвертации HTML → Markdown

________________________________________
Дорожная карта
	Поддержка ZIP-архивов (через JSZip)
	Конвертация DOCX (через mammoth.js)
	Извлечение текста из PDF (через pdf.js)
	Точный подсчёт токенов (tiktoken WASM)
	Прямой экспорт в Pinecone / Weaviate / Chroma
	Пакетная обработка с отдельными файлами на выходе

________________________________________
Автор
Создан Алибеком Исмаиловым (@MavrodiM90) — AI Operations & Automation, Петропавловск, Казахстан.

Если RAGmill сэкономил Вам время — ⭐ на GitHub будет лучшей благодарностью.

