using System;
using System.Collections.Generic;

// Interfaces
interface IUsuario
{
    string Nombre { get; set; }
    string Email { get; set; }
    string Contraseña { get; set; }
    TipoUsuario TipoUsuario { get; set; }
}

interface IVehiculo
{
    string Marca { get; set; }
    string Modelo { get; set; }
    int Año { get; set; }
    bool Disponible { get; set; }
}

interface IAlquiler
{
    IUsuario Cliente { get; set; }
    IVehiculo Vehiculo { get; set; }
    DateTime FechaAlquiler { get; set; }
    DateTime FechaDevolucion { get; set; }
}

// Enumeraciones
enum TipoUsuario
{
    Vendedor,
    Cliente,
    Administrador
}

// Clases
class Usuario : IUsuario
{
    public string Nombre { get; set; }
    public string Email { get; set; }
    public string Contraseña { get; set; }
    public TipoUsuario TipoUsuario { get; set; }
}

class Vehiculo : IVehiculo
{
    public string Marca { get; set; }
    public string Modelo { get; set; }
    public int Año { get; set; }
    public bool Disponible { get; set; }
}

class Alquiler : IAlquiler
{
    public IUsuario Cliente { get; set; }
    public IVehiculo Vehiculo { get; set; }
    public DateTime FechaAlquiler { get; set; }
    public DateTime FechaDevolucion { get; set; }
}

// Clase principal
class Program
{
    static List<IUsuario> usuarios = new List<IUsuario>();
    static List<IVehiculo> vehiculos = new List<IVehiculo>();
    static List<IAlquiler> alquileres = new List<IAlquiler>();
    static IUsuario usuarioActual = null;

    static void Main(string[] args)
    {
        // Inicializar usuarios
        usuarios.Add(new Usuario { Nombre = "Vendedor", Email = "vendedor@carro.com", Contraseña = "123456", TipoUsuario = TipoUsuario.Vendedor });
        usuarios.Add(new Usuario { Nombre = "Cliente", Email = "cliente@carro.com", Contraseña = "123456", TipoUsuario = TipoUsuario.Cliente });
        usuarios.Add(new Usuario { Nombre = "Administrador", Email = "admin@carro.com", Contraseña = "123456", TipoUsuario = TipoUsuario.Administrador });

        // Inicializar vehículos
        vehiculos.Add(new Vehiculo { Marca = "Toyota", Modelo = "Corolla", Año = 2020, Disponible = true });
        vehiculos.Add(new Vehiculo { Marca = "Honda", Modelo = "Civic", Año = 2019, Disponible = true });
        vehiculos.Add(new Vehiculo { Marca = "Ford", Modelo = "Mustang", Año = 2021, Disponible = false });

        // Ciclo de inicio de sesión
        while (true)
        {
            try
            {
                // Inicio de sesión
                usuarioActual = IniciarSesion();

                // Mostrar mensaje de inicio de sesión
                Console.ForegroundColor = ConsoleColor.Green;
                Console.WriteLine($"\nInicio de sesión exitoso como {usuarioActual.Nombre} - {usuarioActual.TipoUsuario}");
                Console.ResetColor();

                // Menú según el tipo de usuario
                if (usuarioActual.TipoUsuario == TipoUsuario.Vendedor)
                {
                    MenuVendedor(usuarioActual);
                }
                else if (usuarioActual.TipoUsuario == TipoUsuario.Cliente)
                {
                    MenuCliente(usuarioActual);
                }
                else if (usuarioActual.TipoUsuario == TipoUsuario.Administrador)
                {
                    MenuAdministrador();
                }
            }
            catch (Exception ex)
            {
                Console.ForegroundColor = ConsoleColor.Red;
                Console.WriteLine(ex.Message);
                Console.ResetColor();
            }
        }
    }

    static IUsuario IniciarSesion()
    {
        Console.WriteLine("\n--- Inicio de sesión ---");
        Console.Write("Ingrese su email: ");
        string email = Console.ReadLine();
        Console.Write("Ingrese su contraseña: ");
        string contraseña = Console.ReadLine();

        IUsuario usuario = usuarios.Find(u => u.Email == email && u.Contraseña == contraseña);

        if (usuario == null)
        {
            throw new Exception("Credenciales inválidas. Intente nuevamente.");
        }

        return usuario;
    }

    static void MenuVendedor(IUsuario vendedor)
    {
        bool salir = false;
        do
        {
            Console.WriteLine("\nMenú Vendedor");
            Console.WriteLine("1. Agregar vehículo");
            Console.WriteLine("2. Alquilar vehículo");
            Console.WriteLine("3. Cerrar sesión");
            Console.Write("Ingrese su opción: ");
            int opcion = int.Parse(Console.ReadLine());

            switch (opcion)
            {
                case 1:
                    AgregarVehiculo();
                    break;
                case 2:
                    AlquilarVehiculo(vendedor);
                    break;
                case 3:
                    Console.WriteLine("Cerrando sesión...");
                    salir = true;
                    break;
                default:
                    Console.WriteLine("Opción inválida");
                    break;
            }
        } while (!salir);
    }

    static void MenuCliente(IUsuario cliente)
    {
        bool salir = false;
        do
        {
            Console.WriteLine("\nMenú Cliente");
            Console.WriteLine("1. Alquilar vehículo");
            Console.WriteLine("2. Ver vehículos disponibles");
            Console.WriteLine("3. Cerrar sesión");
            Console.Write("Ingrese su opción: ");
            int opcion = int.Parse(Console.ReadLine());

            switch (opcion)
            {
                case 1:
                    AlquilarVehiculo(cliente);
                    break;
                case 2:
                    MostrarVehiculosDisponibles();
                    break;
                case 3:
                    Console.WriteLine("Cerrando sesión...");
                    salir = true;
                    break;
                default:
                    Console.WriteLine("Opción inválida");
                    break;
            }
        } while (!salir);
    }

    static void MenuAdministrador()
    {
        bool salir = false;
        do
        {
            Console.WriteLine("\nMenú Administrador");
            Console.WriteLine("1. Ver alquileres");
            Console.WriteLine("2. Cerrar sesión");
            Console.Write("Ingrese su opción: ");
            int opcion = int.Parse(Console.ReadLine());

            switch (opcion)
            {
                case 1:
                    MostrarAlquileres();
                    break;
                case 2:
                    Console.WriteLine("Cerrando sesión...");
                    salir = true;
                    break;
                default:
                    Console.WriteLine("Opción inválida");
                    break;
            }
        } while (!salir);
    }

    static void AgregarVehiculo()
    {
        Console.Write("Ingrese la marca: ");
        string marca = Console.ReadLine();
        Console.Write("Ingrese el modelo: ");
        string modelo = Console.ReadLine();
        Console.Write("Ingrese el año: ");
        int año = int.Parse(Console.ReadLine());

        vehiculos.Add(new Vehiculo { Marca = marca, Modelo = modelo, Año = año, Disponible = true });
        Console.WriteLine("Vehículo agregado correctamente");
    }

    static void AlquilarVehiculo(IUsuario cliente)
    {
        MostrarVehiculosDisponibles();

        Console.Write("Ingrese el índice del vehículo a alquilar: ");
        int indice = int.Parse(Console.ReadLine());

        if (indice >= 0 && indice < vehiculos.Count && vehiculos[indice].Disponible)
        {
            IVehiculo vehiculo = vehiculos[indice];
            vehiculo.Disponible = false;

            Console.Write("Ingrese la fecha de devolución (dd/MM/yyyy): ");
            DateTime fechaDevolucion = DateTime.ParseExact(Console.ReadLine(), "dd/MM/yyyy", null);
            DateTime fechaAlquiler = DateTime.Now;

            alquileres.Add(new Alquiler
            {
                Cliente = cliente,
                Vehiculo = vehiculo,
                FechaAlquiler = fechaAlquiler,
                FechaDevolucion = fechaDevolucion
            });

            Console.WriteLine("Vehículo alquilado correctamente");
        }
        else
        {
            Console.WriteLine("Índice inválido o vehículo no disponible");
        }
    }

    static void MostrarVehiculosDisponibles()
    {
        Console.WriteLine("\nVehículos disponibles:");
        for (int i = 0; i < vehiculos.Count; i++)
        {
            if (vehiculos[i].Disponible)
            {
                Console.WriteLine($"{i}. Marca: {vehiculos[i].Marca}, Modelo: {vehiculos[i].Modelo}, Año: {vehiculos[i].Año}");
            }
        }
    }

    static void MostrarAlquileres()
    {
        Console.WriteLine("\nLista de alquileres:");
        foreach (var alquiler in alquileres)
        {
            Console.WriteLine($"Cliente: {alquiler.Cliente.Nombre}, Vehículo: {alquiler.Vehiculo.Marca} {alquiler.Vehiculo.Modelo}, Fecha Alquiler: {alquiler.FechaAlquiler}, Fecha Devolución: {alquiler.FechaDevolucion}");
        }
    }
}
