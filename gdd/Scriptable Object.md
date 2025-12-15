
#Game 

---
Este tipo de objeto se utiliza para representar una estructura base y de datos inmutables durante la ejecución del juego. 

Ejemplo de scriptable object para un item:

```C#
using UnityEngine;

[CreateAssetMenu(fileName = "Armas", menuName = "Items/objetos/arma")]
public class Armas : ScriptableObject
{
    public string nombre;
    public int daño;
    public GameObject objeto;
}
```

En este ejemplo se puede ver como tenemos la base para un objeto que representara un arma, se puede instanciar desde el menú Items/objetos/arma y que tiene las propiedades de nombre, daño y el GameObject(Prefab) que se debería instanciar.

De esta manera podemos guardar el nombre o id de un objeto y volverlo a instanciar en el caso de cargar partida, en el fichero de guardado deberemos poner la referencia a este scriptable object y todas las propiedades del prefab dinamicas como podrian ser posicion, rotacion etc.