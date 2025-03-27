# laboratorio-CSharp-Excepciones
## Vamos a crear una aplicación de consola que generé un numero aleatorio. La aplicación solicitará al usuario un número, en el caso de que el número introducido sea:

* Mayor mostrará un mensaje: El número es más pequeño.
* Menor mostrará un mensaje: El número es más grande.
  
El usuario dispondrá de 10 intentos para adivinar el número.

1. Controla las excepciones posibles que se pueden producir en la aplicación.

2. Crea una excepción personalizada para lanzarla cuando el número es mayor o menor.

### Solucion:
``` cshrap
public class NumeroMayorException : Exception
{
    public NumeroMayorException(string message) : base(message)
    {
        Console.WriteLine(message);
    }
}
public class NumeroMenorException : Exception
{
    public NumeroMenorException(string message) : base(message)
    {
        Console.WriteLine(message);
    }
}
static void Main(string[] args)
{    

    int intentosInicio = 10;
    int intentos = intentosInicio;
    bool acertado = false;
    Random random = new Random();
    int nrandom = random.Next(1, 100);
    
    //Escribo el numero para facilitar el testeo
    Console.WriteLine(nrandom);
    Console.WriteLine("Se ha generado un numero aleatorio entre 1 y 100. Tienes 10 intentos para adivinarlo.");

        
            while( intentos > 0 && !acertado) {
                try
                {
                    int numero = int.Parse(Console.ReadLine());

                    if (numero < 1 || numero > 100)
                    {
                        throw new ArgumentOutOfRangeException("numero", "El numero debe estar entre 0 y 100.");
                    }
                    if (numero < nrandom)
                    {
                        throw new NumeroMenorException($"Error. El numero aleatorio es mayor.");
                    }
                    else if (numero > nrandom)
                    {
                        throw new NumeroMayorException($"Error. El numero aleatorio es menor.");
                    }
                    else
                    {
                        Console.WriteLine("Felicidades, acertaste!");
                        acertado = true;
                    }
                }
                catch (ArgumentOutOfRangeException ex)
                {
                    Console.WriteLine("Error: '{0}'", ex.Message);
                }
                catch (FormatException ex)
                {
                    Console.WriteLine(ex.Message);
                }
                catch (NumeroMayorException ex)
                {
                    Console.WriteLine($"Te quedan { --intentos} intentos.");
                }
                catch (NumeroMenorException ex)
                {
                    Console.WriteLine($"Te quedan {--intentos} intentos.");
                }

          }
            if (!acertado)
            {
                Console.WriteLine("Te quedaste sin intentos. Fin del juego.");
            }
            else
            {
                Console.WriteLine($"Has ganado el juego en {intentosInicio + 1 - intentos} intentos.");
            }

            Console.ReadLine();

}

