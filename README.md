1. Создаём новый проект
2. Добавялем поле PlaneText, TextView, 2 кнопки "Save" "Load"

![image](https://user-images.githubusercontent.com/38504787/145620253-b3a91a05-6a61-4fa8-be77-7227329b1bd0.png)
3. Назначим имя файла и установим путь для него
~~~ Java
    String filename = "content.txt";
    File file;
    file = new File(MainActivity.this.getFilesDir(),filename);
~~~
4. Напишем обработчик события для кнопки сохранения и загрузки
~~~ Java
public void saveClick(View view) {
        try
        {
            EditText textBox = (EditText) findViewById(R.id.editTextTextPersonName);
            String text = textBox.getText().toString();
            FileOutputStream fos = new FileOutputStream(file);
            fos.write(text.getBytes());
            fos.close();
            Toast.makeText(this, "Текстовый файл успешно сохранён!",
                    Toast.LENGTH_SHORT).show();
        }
        catch (FileNotFoundException e)
        {
            e.printStackTrace();
            Toast.makeText(this, "Файл не найден!",
                    Toast.LENGTH_SHORT).show();
        }
        catch (IOException e)
        {
            e.printStackTrace();
            Toast.makeText(this, "Ошибка сохранения файла!",
                    Toast.LENGTH_SHORT).show();
        }
    }
~~~
~~~ Java
public void openClick(View view) {
        try
        {
            FileInputStream fin = new FileInputStream(file);
            byte[] bytes = new byte[fin.available()];
            fin.read(bytes);
            String text = new String(bytes);
            TextView textView = (TextView) findViewById(R.id.textView);
            textView.setText(text);
            fin.close();
        }
        catch (IOException ex)
        {
            Toast.makeText(this, ex.getMessage(),
                    Toast.LENGTH_SHORT).show();
        }
    }
~~~
5. Установим разрешение на доступ в файле "AndroidManifest.xml"
~~~ XML
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.savereadfile">

    <uses-permission
        android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission
        android:name="android.permission.READ_EXTERNAL_STORAGE"/>
~~~
6. Проверяем
 ![image](https://user-images.githubusercontent.com/38504787/145620945-d4625127-44f5-4942-8ad6-96474fb99395.png)
 ![image](https://user-images.githubusercontent.com/38504787/145620994-2439df7b-b009-4d7a-8bff-61048920d152.png)

