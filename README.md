### Привет, я Георгий

Это описание содержит информацию о моих навыках и проектах, но сначала немного обо мне:

Учусь в "школе 21" от СБЕРА по направлению backend разработки, развиваюсь в направление AI и промпт инжиниринга.<br/>
Также увлечен тестированием и автоматизацией.

Начинал с языка Си, но сейчас основным инструментом является python, в особенности фреймворки для работы с LLM и создания агентов. <br/>
Также начинаю разбираться в java, интересует нагрузочное тестирование.



Чуть ниже карта навыков, она постоянно дополняется, и пока она в процессе разработки, проекты могут быть оформлены не до конца.


```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'fontSize': '14px', 'fontFamily': 'Inter, system-ui, -apple-system, sans-serif' }}}%%
flowchart BT
    c_lang["<div style='text-align: left; padding: 0px; min-width: 270px;'><b>C Language</b> проекты:<br/>• <a href='https://github.com/fanofanapa/matrix_lib_c_edu'>Библиотека для работы с матрицами</a><br/>• <a href='https://github.com/fanofanapa/decimal_lib_c_edu'>Структура данных decimal для Си</a><br/>• <a href='https://github.com/fanofanapa/strings_lib_c_edu'>Своя библиотека string.h</a><br/>• <a href='https://github.com/fanofanapa/cat_grep_educational/tree/main'>Системные утилиты cat grep</a></div>"]
    
    sql["<div style='text-align: left; padding: 4px;'><b>PostgreSQL & SQL</b><br/>• Проектирование и управление БД<br/>• Продвинутые запросы в PL/pgSQL</div>"]

    java["<div style='text-align: left; padding: 4px;'>В работе: <b>Java</b><br/>• Core Java<br/>• Spring Boot<br/>• Hibernate<br/>• Maven / Gradle</div>"]
    
    python["<div style='text-align: left; padding: 0px; min-width: 270px;'><b>Python</b><br/>основной стек:<br/>• FastAPI<br/>• LangChain<br/>• HTTPX / REST APIs<br/>• JSON / Pydantic<br/><b>Проекты:</b><br/>• <a href='https://github.com/fanofanapa/events_alert_public'>Бот мониторинга промо-акций через открытое API</a><br/>• <a href='https://github.com/fanofanapa/sberEduHackathon'>Финалист хакатона: приложение для помощи учителю, создает варианты заданий с AI</a> </div>"]

    c_lang --> python
    c_lang -.-> java

    %% Минималистичный стиль узлов: светлый фон, темные тонкие рамки, скругленные углы (rx/ry)
    classDef default fill:#fafafa,stroke:#262626,stroke-width:1.5px,color:#171717,rx:8px,ry:8px;
    
    %% Строгий стиль линий
    linkStyle default stroke:#737373,stroke-width:1.5px;
    style java stroke-dasharray: 5 5;
```
