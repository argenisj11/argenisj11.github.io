
# **Reglas de Programación para el Proyecto SIMON FORM** *(Basado en Convenciones Microsoft)*  

---

## **1. Convenciones de Nombres**  

### **1.1. Variables**  
- **camelCase** para variables locales y parámetros:  
  ```csharp
  int idUsuario = 1;
  string nombreFormulario = "Login";
  ```
- **PascalCase** para propiedades y campos públicos:  
  ```csharp
  public string NombreCompleto { get; set; }
  ```
- **Prefijo `_`** para campos privados:  
  ```csharp
  private string _conexionBD;
  ```

### **1.2. Clases y Métodos**  
- **PascalCase** para clases, métodos y espacios de nombres:  
  ```csharp
  public class FormularioPrincipal { }
  public void ProcesarDatos() { }
  ```
- **Interfaces** deben llevar prefijo `I`:  
  ```csharp
  public interface IFormularioService { }
  ```

### **1.3. Constantes y Enums**  
- **MAYÚSCULAS_CON_GUION_BAJO** para constantes:  
  ```csharp
  public const int TIEMPO_ESPERA = 5000;
  ```
- **PascalCase** para enums:  
  ```csharp
  public enum EstadoFormulario { Activo, Inactivo }
  ```

---

## **2. Organización del Código**  

### **2.1. Estructura de Carpetas**  
```
SIMON_FORM/
├── Forms/          # Formularios WinForms
├── Models/         # Modelos de datos
├── Services/       # Lógica de negocio
├── Utils/          # Herramientas auxiliares
└── Program.cs      # Punto de entrada
```

### **2.2. Orden en Clases**  
1. **Campos privados**  
2. **Constructores**  
3. **Propiedades públicas**  
4. **Métodos públicos**  
5. **Métodos privados**  
6. **Eventos**  
7. **Clases anidadas**  

**Ejemplo:**  
```csharp
public class EjemploClase {
    private int _contador;
    
    public EjemploClase() { }
    
    public int Id { get; set; }
    
    public void MetodoPublico() { }
    
    private void MetodoPrivado() { }
}
```

---

## **3. Estilo de Código**  

### **3.1. Formato Básico**  
- **4 espacios** (no tabs).  
- **Llaves `{}`** siempre, incluso en bloques de una línea:  
  ```csharp
  if (condicion) {
      Accion();
  }
  ```


### **3.2. Expresiones y Operadores**  
- **Espacios alrededor de operadores**:  
  ```csharp
  int resultado = a + b;
  ```
- **Expresiones lambda claras**:  
  ```csharp
  var filtrados = lista.Where(x => x.EsActivo);
  ```

### **3.3. Comentarios y Documentación**  
- **XML Docs** en métodos públicos:  
  ```csharp
  /// <summary>
  /// Valida si un usuario existe.
  /// </summary>
  /// <param name="id">ID del usuario</param>
  /// <returns>True si existe</returns>
  public bool ValidarUsuario(int id) { }
  ```
- **Evitar comentarios obvios**, solo explicar lógica compleja.  

---

## **4. Manejo de Excepciones**  

### **4.1. Try-Catch con Filtros**  
```csharp
try {
    ProcesarFormulario();
}
catch (SqlException ex) when (ex.Number == 1205) {
    // Manejar deadlock específico
}
catch (Exception ex) {
    _logger.LogError(ex, "Error inesperado");
    throw;  // Preservar stack trace
}
```

### **4.2. Excepciones Personalizadas**  
```csharp
public class FormularioException : Exception {
    public int CodigoError { get; }
    
    public FormularioException(string mensaje, int codigo) : base(mensaje) {
        CodigoError = codigo;
    }
}
```

---

## **5. Async/Await**  

### **5.1. Nomenclatura y Buenas Prácticas**  
- **Sufijo `Async`** en métodos asíncronos:  
  ```csharp
  public async Task<List<Usuario>> ObtenerUsuariosAsync() { }
  ```
- **Evitar `async void`** (solo para eventos).  

### **5.2. Uso Correcto**  
```csharp
public async Task ProcesarAsync() {
    var datos = await _servicio.ObtenerDatosAsync();
    await _repo.GuardarAsync(datos);
}
```

---

## **6. Seguridad**  

### **6.1. Validación de Inputs**  
- **Siempre validar parámetros**:  
  ```csharp
  public void Procesar(string input) {
      if (string.IsNullOrEmpty(input))
          throw new ArgumentNullException(nameof(input));
  }
  ```
- **Protección contra SQL Injection** (usar parámetros):  
  ```csharp
  using (var conn = new SqlConnection(_connString)) {
      var query = "SELECT * FROM Usuarios WHERE Id = @id";
      await conn.QueryAsync(query, new { id = usuarioId });
  }
  ```

### **6.2. Hash de Contraseñas**  
```csharp
public string HashPassword(string password) {
    var salt = GenerateSalt();
    var hash = PBKDF2(password, salt);
    return $"{salt}.{hash}";
}
```

---

## **7. Integración con VB6**  

### **7.1. Llamada desde VB6**  
```vb
' Declaración
Private Declare Function LlamarFormulario Lib "SimonForm.dll" (ByVal idForm As String, ByVal idUser As String) As Long

' Uso
Call LlamarFormulario("FRM001", "USR123")
```

### **7.2. Manejo en C#**  
```csharp
public static void Main(string[] args) {
    if (args.Length < 2) {
        MostrarError("Faltan parámetros");
        return;
    }
    var idForm = args[0];
    var idUser = args[1];
    // Lógica...
}
```

---

## **8. Pruebas Unitarias**  

### **8.1. Convenciones xUnit**  
```csharp
[Fact]
public void Sumar_DosNumerosPositivos_RetornaSumaCorrecta() {
    var resultado = Calculadora.Sumar(2, 3);
    Assert.Equal(5, resultado);
}
```

### **8.2. Buenas Prácticas**  
- **Nombres descriptivos** (`[Método]_[Escenario]_[Resultado]`).  
- **Mocking con Moq**:  
  ```csharp
  var mockRepo = new Mock<IUsuarioRepository>();
  mockRepo.Setup(x => x.Obtener(1)).Returns(new Usuario());
  ```

---

## **9. Referencias**  
🔹 [Convenciones de C# - Microsoft](https://learn.microsoft.com/es-es/dotnet/csharp/fundamentals/coding-style/coding-conventions)
