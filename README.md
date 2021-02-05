# PhoneBook Android 

_Aplicación móvil nativa de Agenda de contactos._

## Comenzando 🚀

_Estas instrucciones te permitirán obtener una copia del proyecto en funcionamiento en tu máquina local para propósitos de desarrollo y pruebas._

Mira **Deployment** para conocer como desplegar el proyecto, también puedes probar directamente la app, descárgala de aquí 
https://github.com/EzqTrujillo55/phonebook-android/blob/master/ContactsBook.apk

### Pre-requisitos 📋

_Android Studio_


### Instalación 🔧

```
1. Ejecutar el siguiente comando: git clone url de este repositorio
2. Abrir el proyecto en Android Studio
3. Click en el icono de ejecución. 
4. Importante haber creado antes dispositivos virtuales para ver la app en ejecución o conectar un dispositivo físico con la depuración USB Activada
```


## Despliegue 📦

```
1. En android studio click en Build, luego en Generate signed bundle / apk
2. Seguir los pasos del asistente
```


## Funcionalidades 📖
1. Lectura y listado de datos
    ```
     //Dentro de la función onCreate especificamos el listener para el ListView
     //Obtenemos el objeto ListPerson
     //A dicho objeto le asignamos el contenido del ArrayAdapter
     //Creamos la referencia a People
     //Asignamos un Listener a People, y con los métodos onChildAdded y onChildChanged, veirificamos constantemente la información de la BDD
        final ArrayAdapter<String> myArrayAdapter = new ArrayAdapter<String>(MainActivity.this, android.R.layout.simple_list_item_1, myArrayList);
        myListView = (ListView) findViewById(R.id.listPerson);
        myListView.setAdapter(myArrayAdapter);
        mRef = FirebaseDatabase.getInstance().getReference().child("People");
        mRef.addChildEventListener(new ChildEventListener() {
            @Override
            public void onChildAdded(@NonNull DataSnapshot snapshot, @Nullable String previousChildName) {
                String value = snapshot.getValue(String.class);
                myArrayList.add(value);
                myArrayAdapter.notifyDataSetChanged();
            }

            @Override
            public void onChildChanged(@NonNull DataSnapshot snapshot, @Nullable String previousChildName) {
                myArrayAdapter.notifyDataSetChanged();
            }
    ```
2. Agregar contactos 
    ```
    //Obtenemos el botón de agregar
    //Invocamos el listener, que genera un número randómico para el id del registro
    //Obtenemos el contenido del Input, lo convertimos a String y retiramos los espacios laterales
    //Establece la referencia y almacena el nombre digitado
    btn = (Button)findViewById(R.id.buttonAgregar);
        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                int min = 1;
                int max = 1000;
                txt = (TextInputLayout) findViewById(R.id.txtNombre);
                String nombre = txt.getEditText().getText().toString().trim();
                int random_id = (int)(Math.random() * (max - min + 1) + min);
                String random_id_string = String.valueOf(random_id);
                mRef = FirebaseDatabase.getInstance().getReference("People").child(random_id_string);
                mRef.setValue(nombre);
            }
        });
    ```
3. Selección de contacto. 
    ```
        //Obtenemos el objeto listPerson
        //Invocamos el listener para la selección de un item
        //Inbocamos el método getItemAtPosition() para obtener el contenido del item clickeado
        //Colocamos el contenido obtenido en el Input
        myListView = (ListView) findViewById(R.id.listPerson);
        myListView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                String selectedFromList = (String) myListView.getItemAtPosition(position);
                txt = (TextInputLayout) findViewById(R.id.txtNombre);
                txt.getEditText().setText(selectedFromList);
            }
        });
    ```
 
## Preview
![Screenshot](preview.jpeg)


## Video Demostrativo
https://drive.google.com/file/d/10H5-D0sXGkmYVzOTDaxQBtWhpacmmY9T/view?usp=drivesdk

## Construido con 🛠️

_Menciona las herramientas que utilizaste para crear tu proyecto_

* [Android Studio](https://developer.android.com/studio) - Entorno de desarrollo para aplicaciones nativas
* [Java](https://www.java.com/es/download/) - Lenguaje de programación empleado para aplicaciones nativas con Android


## Autores ✒️

* **Gabriela García** - *Codificación, Investigación, Documentación* - [Gabiita](https://github.com/Gabiita)
* **Pablo Trujillo** - *Codificación, Investigación, Documentación* - [EzqTrujillo55](https://github.com/EzqTrujillo55)
* **Danny Guañuna** - *Codificación, Investigación, Documentación* - [DannyGua](https://github.com/Dannygua/EjerciciosAS)
* **Wester Mendoza** - *Codificación, Investigación, Documentación* - [JoelMendoza1](https://github.com/JoelMendoza1)
