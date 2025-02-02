# Инсталяция

Данная сборка предназначена для разворачивания проекта на Laravel монолитной архитектуры.
Запуск фронтенда осуществляется локально, запуск Laravel 

# Стек:
- PHP 8.3
- Laravel 11
- PosgresSQL 16
- Vuejs 3
- Vite
- Docker



# Начало

Убедитесь, что у вас есть composer и глобально установлен пакет установщик Laravel.
Если нет композера, то установите его или можете сразу перейти к шагу с установкой Laravel в src

### Для Mac Os
```bash
/bin/bash -c "$(curl -fsSL https://php.new/install/mac/8.3)"
```

### Для Linux
```bash
/bin/bash -c "$(curl -fsSL https://php.new/install/linux/8.3)"
```

Далее установите глобально установщик Laravel. Это нужно сделать один раз
composer global require laravel/installer

Выполните команду для создания приложения. Laravel создаст директория src и туда установит Laravel


### Создание Laravel
```bash
laravel new laravel
```

После скачивания проекта, необходимо внести корректировку в переменную среды  .env

```jsunicoderegexp
DB_CONNECTION=pgsql
DB_HOST=localhost
DB_PORT=5432
DB_DATABASE=laravel_db
DB_USERNAME=root
DB_PASSWORD=root
```

и заменить франение сессии в файле

```jsunicoderegexp
SESSION_DRIVER=file
```

Далее необходимо установить пакеты для фронтенда

Устанавливаем vite

```bash
cd laravel
npm install
npm install vue@3
npm install @vitejs/plugin-vue --save-dev
```

Далее модифицируем vite.config.js под нашу сборку

```jsunicoderegexp
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import vue from '@vitejs/plugin-vue';

export default defineConfig({
    plugins: [
        vue({
            template: {
                transformAssetUrls: {
                    base: null,
                    includeAbsolute: false,
                },
            },
        }),
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
    ],
    build: {
        outDir: 'public/dist',
    },
    resolve: {
        alias: {
            vue: 'vue/dist/vue.esm-bundler.js',
        },
    },
});
```

Запускаем сборку фронта
```bash
cd laravel
npm run dev
```
Запускаем сборку проекта на докер
```bash
docker compose up -d --build
```

Остановка докера
```bash
docker compose down -v
```
