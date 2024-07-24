## Aider: настройка фидбека от линтера/билдера

Автор: [Родион Мостовой](https://t.me/rodion_m_tg)

Обсуждения в клубе: https://t.me/c/2069889012/6/4497

---

Фидбек от линтера/компилятора/интерпретатора может существенно улучшить выхлоп от LLM через итеративный подход. Andrew Ng об этом рассказывал в своем [небольшом выступлении](https://www.youtube.com/watch?v=sal78ACtGTc). 

**Настройка для TypeScript/JavaScript**

Оптимальные настройки команды `lint` и `test` для **TypeScript/JavaScript** проекта, к которым я пришел на текущий момент:
``` cmd
lint-cmd: "npx @biomejs/biome lint --write "
auto-lint: true

test-cmd: "cd code-search-ui && npx @biomejs/biome format --write ./src && npm run build"
auto-test: true
```
Тут используется линтер [biome](https://biomejs.dev/linter/) вместо eslint (его надо установить сначала), мне он показался проще + у него очень подробные сообщения об ошибках + безопасные автофиксы. Еще, в `test-cmd` тут запускается не только билд, но и форматирование. Сюда же можно добавить и запуск тестов если у вас они есть, но тогда `test-cmd` станет еще дороже.

**Настройка для C# (.NET):**
``` yml
test-cmd: "dotnet build" # && dotnet test (optionally)
auto-test: true
```

Нормально настроить точечный линтер для C# пока так и не удалось из-за ограничений в библиотеке [csharpier](https://csharpier.com/docs/CLI). Ждем эту [issue](https://github.com/belav/csharpier/issues/1131) пока сделают корректный exit code.

PS: [Вот](https://github.com/paul-gauthier/aider/issues/907) моя новая Issue в aider с предложением добавить отдельную команду для авто-форматирования измененных файлов.
