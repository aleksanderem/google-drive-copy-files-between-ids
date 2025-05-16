
# 📁 Google Drive Folder Copier (Google Colab)

This notebook allows recursive copying of one Google Drive folder to another. It supports:
- Google account authorization,
- skipping existing files and folders in the destination directory,
- preserving folder structure during copy,
- handling timeouts and retry logic.

## 🧰 Requirements

- [Google Colab](https://colab.research.google.com/)
- Google account with access to both source and destination folders

## 🚀 How to use

### 1. Install required libraries

Run the first cell in the notebook to install the necessary packages:

```python
!pip install --upgrade google-api-python-client google-auth-httplib2 google-auth-oauthlib
```

### 2. Provide folder IDs

At the end of the main code cell, update these variables:

```python
source_folder_id = 'SOURCE_FOLDER_ID'
target_folder_id = 'TARGET_FOLDER_ID'
```

You can find the folder ID in its URL:  
`https://drive.google.com/drive/folders/<ID>`

### 3. Run the copy cell

- After clicking "Play", you'll be prompted to authorize your Google account.
- The script will scan both folders.
- It will copy only missing files and folders (skipping existing ones).
- Folders are processed recursively.
- In case of errors (e.g., API timeouts), the script retries up to 5 times.

## 🧠 How it works

- `get_existing_items()` fetches existing files in the destination folder to avoid duplicates.
- `copy_contents()` walks through the source folder and only copies new items.
- Folders are processed recursively.
- `safe_copy()` prevents crashes by retrying with increasing delay (`sleep(2^n)`).

## 📝 Example

```python
source_folder_id = '1gTqnEeQ21mLG1As5CDjLX0sNtgNIXtyy'
target_folder_id = '1by-hP_GqRz-W4Z5sKGo02yyYFDBz0SYp'

copy_drive_folder_between_ids(source_folder_id, target_folder_id)
```

## 💡 Tips

- You can safely stop and re-run the script — it will skip already copied files.
- Copying may take time due to Google Drive API limits.
- Works with all file types including Google Docs, Sheets, etc.

## 🔐 Permissions

The notebook uses `google.colab.auth.authenticate_user()` for secure login via Google's official auth window. No data is saved or stored outside the Colab session.

---

# 📁 Kopiowanie folderów Google Drive (Google Colab)

Ten notebook służy do rekurencyjnego kopiowania zawartości folderu w Google Drive do innego folderu. Obsługuje:
- autoryzację konta Google,
- pomijanie istniejących plików i folderów w katalogu docelowym,
- kopiowanie z zachowaniem struktury folderów,
- obsługę timeoutów oraz automatyczne ponawianie prób.

## 🧰 Wymagania

- Środowisko [Google Colab](https://colab.research.google.com/)
- Konto Google z dostępem do źródłowego i docelowego folderu w Google Drive

## 🚀 Jak używać

### 1. Zainstaluj wymagane biblioteki

Uruchom pierwszą komórkę w notebooku, aby zainstalować niezbędne pakiety:

```python
!pip install --upgrade google-api-python-client google-auth-httplib2 google-auth-oauthlib
```

### 2. Uzupełnij ID folderów

Na końcu głównej komórki uzupełnij:

```python
source_folder_id = 'ID_FOLDERU_ŹRÓDŁOWEGO'
target_folder_id = 'ID_FOLDERU_DOCZELOWEGO'
```

ID folderu znajdziesz w jego adresie URL:  
`https://drive.google.com/drive/folders/<ID>`

### 3. Uruchom komórkę kopiującą

- Po kliknięciu "Play" zostaniesz poproszony o autoryzację konta Google.
- Skrypt przeskanuje oba foldery.
- Skopiuje tylko brakujące pliki i foldery.
- Foldery są przetwarzane rekurencyjnie.
- W przypadku błędów kopiowania, próby są automatycznie ponawiane.

## 🧠 Jak to działa?

- `get_existing_items()` pobiera listę plików w folderze docelowym.
- `copy_contents()` iteruje przez folder źródłowy i kopiuje tylko brakujące elementy.
- Foldery są kopiowane rekurencyjnie.
- `safe_copy()` zabezpiecza kopiowanie przed błędami przez ponawianie prób z narastającym opóźnieniem (`sleep(2^n)`).

## 📝 Przykład użycia

```python
source_folder_id = '1gTqnEeQ21mLG1As5CDjLX0sNtgNIXtyy'
target_folder_id = '1by-hP_GqRz-W4Z5sKGo02yyYFDBz0SYp'

copy_drive_folder_between_ids(source_folder_id, target_folder_id)
```

## 💡 Wskazówki

- Można bezpiecznie zatrzymać i ponownie uruchomić skrypt — pominie pliki, które już zostały skopiowane.
- Kopiowanie może trochę potrwać — Google API ma limity zapytań.
- Działa ze wszystkimi typami plików (Google Docs, PDF, obrazy itd.).

## 🔐 Uprawnienia

Notebook wykorzystuje `google.colab.auth.authenticate_user()` do bezpiecznego logowania poprzez oficjalne okno autoryzacji Google. Żadne dane nie są zapisywane poza sesją Colab.

---
