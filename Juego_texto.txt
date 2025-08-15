import kotlin.random.Random; //Importar random (?) que loco


fun main() {
    val numero_generado: Int = Random.nextInt(0,100); //Generar el numero por la computadora
    var intentos: Int = 0; 
    var respuesta = -1;                         //Inicializando la respuesta como -1 para que NO se cierre el juego si fuera el mismo numero al generado e inicializar el loop
    
    while(numero_generado != respuesta){        //Compara el numero generado con la respuesta
        respuesta = validar_numero_entrada();  //Checar si es valido
        intentos += verificar_numero(respuesta, numero_generado); //Checar si es el mismo numero mientras aumenta los intentos, le mandamos la respuesta y el numero random
        println("Numero de intentos ${intentos}");
    }
    
    //Mensaje de victoria para cuando termine el while
    println("");
    println("Es el mismo numero! ${respuesta}, Ganaste !!");
    println("");
    println("Numero de intentos: ${intentos}");
}

//Checar si la respuesta ingresada es un numero, no valida espacios vacios ni caracteres

fun validar_numero_entrada(): Int{
    var respuesta: String? = null;              //Checar a ver si la respuesta tiene caracteres
    var respuesta_valida: Int? = null;          //Tener la respuesta final en entero, inicializa en null

    print("Por favor introduce un numero del 0 al 100 sin punto decimal");
    println("");
    
    while(true){
        respuesta = readlnOrNull();             //leer lo que se introduce, si no hay nada, lo considera null
        if(respuesta == null){                  //Si se convierte en null, no pasa y vuelve a iniciar el loop
            println("No se que intentase hacer, por favor vuelve a intentar"); 
            continue;                           //Salta todo lo demas
        }
        
        respuesta_valida = respuesta!!.toIntOrNull();   // !! Asegura que la respuesta va existir, checa si es un numero, sino lo convierte a null
        if(respuesta_valida == null){                   //Si se convierte en null, no pasa y vuelve a iniciar el loop
            println("Eso que introdujiste no lo puedo leer como numero, por favor intenta escribir un numero");
            continue;                                   //Salta todo lo demas
        }
        
        if(respuesta_valida!! > 100 || respuesta_valida!! < 0){          //Por ultimo verifica que este dentro del rango de 0 a 100
            println("Ese numero esta fuera de rango, introduce un numero entre 0 y 100");
        }
        else{
            return respuesta_valida!!; //Si cumple con el rango, regresa el numero como un entero para el siguiente paso
        }
    }
    return 0; //Terminar funcion
}


//Funcion para verificar si el numero coincide con el de la computadora
fun verificar_numero(numero_recibido: Int, numero_generado: Int): Int{      //Recibe la respuesta ya validada y el numero generado
    if(numero_recibido!! > numero_generado){                                //Si el numero es mayor
        println("Incorrecto!");
        println("El numero introducido es MAYOR al numero aleatorio");
    }
    if(numero_recibido!! < numero_generado){                                //Si el numero es menor
        println("Incorrecto!");
        println("El numero introducido es MENOR al numero aleatorio");
    }
    return 1; //Retorna 1 para que se vaya sumando al numero de intentos
}