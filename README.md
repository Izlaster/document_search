Ниже приведена подробная инструкция по установке и запуску pyenv, Python 3.10, Poetry и Jupyter Notebook под Ubuntu. Следуйте этим шагам:

---

## 1. Установка зависимостей для сборки Python

Перед установкой pyenv и компиляцией Python, убедитесь, что у вас установлены необходимые системные библиотеки:

```bash
sudo apt update
sudo apt install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev \
    libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev \
    python-openssl git
```

---

## 2. Установка pyenv

pyenv позволяет легко устанавливать и управлять разными версиями Python. Для установки выполните следующие команды:

1. Склонируйте репозиторий pyenv:
   ```bash
   curl https://pyenv.run | bash
   ```
   
2. Добавьте пути pyenv в ваш shell. Если вы используете bash, отредактируйте файл `~/.bashrc` (или `~/.bash_profile`):

   ```bash
   # Добавьте в конец файла ~/.bashrc
   export PATH="$HOME/.pyenv/bin:$PATH"
   eval "$(pyenv init --path)"
   eval "$(pyenv init -)"
   eval "$(pyenv virtualenv-init -)"
   ```

3. Примените изменения:
   ```bash
   source ~/.bashrc
   ```
   
   После этого убедитесь, что pyenv установлен, выполнив:
   ```bash
   pyenv --version
   ```

---

## 3. Установка Python 3.10 с помощью pyenv

1. Сначала посмотрите доступные версии Python:
   ```bash
   pyenv install --list | grep 3.10
   ```

2. Установите нужную версию (например, 3.10.11):
   ```bash
   pyenv install 3.10.11
   ```

3. Сделайте её глобальной (или установите для проекта локально):
   ```bash
   pyenv global 3.10.11
   ```
   
4. Проверьте версию Python:
   ```bash
   python --version
   ```

---

## 4. Установка Poetry

Poetry — это инструмент для управления зависимостями и упаковки Python-проектов. Для установки выполните:

1. Скачайте и установите Poetry:
   ```bash
   curl -sSL https://install.python-poetry.org | python3 -
   ```

2. Добавьте Poetry в PATH (по умолчанию он устанавливается в `$HOME/.local/bin`):
   ```bash
   echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
   source ~/.bashrc
   ```

3. Проверьте установку:
   ```bash
   poetry --version
   ```

---

## 5. Настройка вашего проекта с помощью Poetry

В корне вашего проекта должен быть файл `pyproject.toml` (как указано в вашем примере). Для установки зависимостей выполните:

1. Перейдите в папку с проектом:
   ```bash
   cd /path/to/your/project
   ```

2. Установите зависимости:
   ```bash
   poetry install
   ```

   Poetry создаст виртуальное окружение и установит все пакеты, указанные в `pyproject.toml`.

---

## 6. Запуск Jupyter Notebook через Poetry

Чтобы запустить Jupyter Notebook в контексте виртуального окружения, выполните:

   ```bash
   poetry run jupyter notebook
   ```

   После этого откроется браузер с интерфейсом Jupyter, где вы сможете работать с ноутбуками.

---

## Результаты

В Jupyter Notebook будут показаны следующие файлы:

- **GarantAnalysis.ipynb** аналитика по текстам.
- **BERT_Vector_Default.ipynb** использует модель BERT для создания векторных представлений текстов (эмбеддингов) и построения FAISS-индекса для быстрого поиска похожих текстов.
- **BERT_Vector_UpgradeChunks.ipynb** является улучшенной версией **BERT_Vector_Default.ipynb**, где добавлена функция разбиения длинных текстов на чанки для более эффективного создания эмбеддингов.
- **TestingModel_Default.ipynb** предназначен для тестирования модели, созданной в **BERT_Vector_Default.ipynb**.
- **TestingModel_UpgradeChunks.ipynb**Этот файл предназначен для тестирования улучшенной модели, созданной в **BERT_Vector_UpgradeChunks.ipynb**.

Если потребуется выйти из Poetry-окружения, просто введите команду `exit` в терминале.
