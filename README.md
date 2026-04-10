# | PRE- PARCIAL ECI SPORT LIFE |
#### Dana Valeria Leal Guzmán

## PARTE TEÓRICA
**1.Identifique las funcionalidades que se piden para el sistema de SportLife y listelas en una matriz de trazabilidad que le permita entender cuáles son las más prioritarias, cuáles son las que bloquean a otras o son derivadas de otras funcionalidades.**

MATRIZ DE TRAZABILIDAD = organizar funcionalidades + prioridad + dependencias

| ID | Funcionalidad              | Prioridad | Depende de              | Tipo        |
|----|----------------------------|----------|--------------------------|-------------|
| F1 | Registro de usuario        | Alta     | Ninguna                  | Base        |
| F2 | Login                      | Alta     | F1                       | Base        |
| F3 | Listar productos           | Alta     | Ninguna                  | Base        |
| F4 | Ver detalle de producto    | Media    | F3                       | Derivada    |
| F5 | Agregar al carrito         | Alta     | F2, F3                   | Crítica     |
| F6 | Ver carrito                | Alta     | F5                       | Derivada    |
| F7 | Generar orden              | Alta     | F6                       | Crítica     |
| F8 | Procesar pago              | Alta     | F7                       | Crítica     |

**BASE =** Son las que no dependen de nadie
**DERIVADA =** Son las que no dependen de nadie
**CRÍTICA =** Son funcionalidades que dependen de otra pero no son críticas

**2.Para cada una de las funcionalidades previamente identificadas mencione:**

- POST → crear → NO idempotente 
- GET → consultar → SI idempotente 
- PUT → actualizar → SI idempotente 
- DELETE → eliminar → SI idempotente
- IDEMPOTENTE →  


**a. Tipo de verbo HTTP**
- F1 = POST /users
- F2 = POST /auth/login
- F3 = GET /products
- F4 = GET /products/{id}
- F5 = POST /cart
- F6 = GET /cart
- F7 = POST /orders
- F8 = POST /payments

**b y c. Establezca si es una funcionalidad idempotente o no y Cuál es la razón técnica de su decisión.**
- F1: No es idempotente ya que cada ejecución crea un nuevo usuario en el sistema.
- F2: No es idempotente ya que cada ejecución genera un proceso de autenticación que puede producir un nuevo token o sesión.
- F3: Es idempotente ya que solo consulta el listado de productos sin modificar el estado del sistema.
- F4: Es idempotente ya que únicamente consulta la información de un producto específico sin alterar datos.
- F5: No es idempotente ya que cada ejecución modifica el carrito agregando productos.
- F6: Es idempotente ya que solo consulta el contenido del carrito sin modificarlo.
- F7: No es idempotente ya que cada ejecución genera una nueva orden de compra.
- F8: No es idempotente ya que cada ejecución procesa una transacción de pago que altera el estado del sistema.


**d. Mencione sus datos de entrada y de salida (Establezca de qué tipo es cada propiedad y si es obligatorio o no)**

**d. Inputs y Outputs**

**F1 – Registro de usuario**

Input:

| Campo     | Tipo   | Obligatorio |
|----------|--------|------------|
| name     | String | Sí         |
| email    | String | Sí         |
| password | String | Sí         |

Output:

| Campo | Tipo    |
|------|---------|
| id   | Integer |
| name | String  |
| email| String  |

---

**F2 – Login**

Input:

| Campo    | Tipo   | Obligatorio |
|---------|--------|------------|
| email   | String | Sí         |
| password| String | Sí         |

Output:

| Campo | Tipo   |
|------|--------|
| token| String |

---

**F3 – Listar productos**

Input:

| Campo     | Tipo   | Obligatorio |
|----------|--------|------------|
| category | String | No         |
| name     | String | No         |

Output:

| Campo  | Tipo    |
|-------|---------|
| id    | Integer |
| name  | String  |
| price | Double  |
| stock | Integer |

---

**F4 – Ver producto**

Input:

| Campo     | Tipo    | Obligatorio |
|----------|---------|------------|
| productId| Integer | Sí         |

Output:

| Campo       | Tipo    |
|------------|---------|
| id         | Integer |
| name       | String  |
| description| String  |
| price      | Double  |
| stock      | Integer |

---

**F5 – Agregar al carrito**

Input:

| Campo      | Tipo    | Obligatorio |
|-----------|---------|------------|
| productId | Integer | Sí         |
| quantity  | Integer | Sí         |

Output:

| Campo   | Tipo   |
|--------|--------|
| message| String |

---

**F6 – Ver carrito**

Input:

| Campo  | Tipo    | Obligatorio |
|-------|---------|------------|
| userId| Integer | Sí         |

Output:

| Campo    | Tipo   |
|---------|--------|
| products| List   |
| total   | Double |

---

**F7 – Generar orden**

Input:

| Campo  | Tipo    | Obligatorio |
|-------|---------|------------|
| cartId| Integer | Sí         |

Output:

| Campo  | Tipo    |
|-------|---------|
| orderId| Integer|
| total | Double  |

---

**F8 – Procesar pago**

Input:

| Campo          | Tipo    | Obligatorio |
|---------------|---------|------------|
| orderId       | Integer | Sí         |
| paymentMethod | String  | Sí         |

Output:

| Campo         | Tipo    |
|--------------|---------|
| status       | String  |
| transactionId| String  |

**e. De un ejemplo de cómo se vería la entrada y la salida.**

**F1 – Registro**

    Entrada:
    {
    "name": "Dana",
    "email": "dana@gmail.com",
    "password": "123456"
    }

    Salida:
    {
    "id": 1,
    "name": "Dana",
    "email": "dana@gmail.com"
    }

---

**F2 – Login**

    Entrada:
    {
    "email": "dana@gmail.com",
    "password": "123456"
    }

    Salida:
    {
    "token": "abc123xyz"
    }

---

**F3 – Listar productos**

    Salida:
    [
    {
    "id": 1,
    "name": "Zapatos Running",
    "price": 120000,
    "stock": 10
    }
    ]

---

**F4 – Ver producto**

    Salida:
    {
    "id": 1,
    "name": "Zapatos Running",
    "description": "Alta calidad",
    "price": 120000,
    "stock": 10
    }

---

**F5 – Agregar al carrito**

    Entrada:
    {
    "productId": 1,
    "quantity": 2
    }

    Salida:
    {
    "message": "Producto agregado"
    }

---

**F6 – Ver carrito**

    Salida:
    {
    "products": [
    {
    "name": "Zapatos Running",
    "quantity": 2
    }
    ],
    "total": 240000
    }

---

**F7 – Generar orden**

    Salida:
    {
    "orderId": 10,
    "total": 240000
    }

---

**F8 – Procesar pago**

    Entrada:
    {
    "orderId": 10,
    "paymentMethod": "CARD"
    }

    Salida:
    {
    "status": "PAID",
    "transactionId": "TX123"
    }

**f. Establezca qué validaciones de input y el negocio debe tener en
cuenta.**

**f. Validaciones de input y negocio**

**F1 – Registro**
- Email válido
- Password mínimo 6 caracteres
- Email no registrado previamente

**F2 – Login**
- Usuario existente
- Password correcta

**F3 – Listar productos**
- Filtros válidos (si se envían)

**F4 – Ver producto**
- Producto existe
- Producto activo

**F5 – Agregar al carrito**
- Producto existe
- Stock disponible
- Cantidad mayor a 0

**F6 – Ver carrito**
- Usuario autenticado
- Carrito existente

**F7 – Generar orden**
- Carrito no vacío
- Productos disponibles en stock

**F8 – Procesar pago**
- Orden válida
- Orden no pagada previamente
- Método de pago válido

**g. Establezca los códigos HTTP y mensaje para Happy Path y Flujo de
Error**

**g. Códigos HTTP y mensajes**

**F1 – Registro**
- 201 CREATED → Usuario creado correctamente
- 400 BAD REQUEST → Datos inválidos
- 409 CONFLICT → Email ya registrado

**F2 – Login**
- 200 OK → Autenticación exitosa
- 401 UNAUTHORIZED → Credenciales incorrectas

**F3 – Listar productos**
- 200 OK → Lista obtenida correctamente
- 400 BAD REQUEST → Filtros inválidos

**F4 – Ver producto**
- 200 OK → Producto encontrado
- 404 NOT FOUND → Producto no existe

**F5 – Agregar al carrito**
- 200 OK → Producto agregado
- 400 BAD REQUEST → Datos inválidos
- 404 NOT FOUND → Producto no existe
- 409 CONFLICT → Sin stock

**F6 – Ver carrito**
- 200 OK → Carrito obtenido
- 404 NOT FOUND → Carrito no existe

**F7 – Generar orden**
- 201 CREATED → Orden generada
- 400 BAD REQUEST → Carrito inválido

**F8 – Procesar pago**
- 200 OK → Pago exitoso
- 402 PAYMENT REQUIRED → Pago rechazado
- 400 BAD REQUEST → Datos inválidos

**3. Genere el diagrama de componentes general del sistema SportLife**
<img width="886" height="504" alt="Captura de pantalla 2026-04-10 005531" src="https://github.com/user-attachments/assets/feaf0928-252a-47a8-af46-690b4b22e37f" />

**6. Modelo de base de datos relacional**

Tablas:

- users (id, name, email, password)
- products (id, name, price, stock)
- cart (id, user_id)
- cart_items (id, cart_id, product_id, quantity)
- orders (id, user_id, total, status)
- payments (id, order_id, amount, status)

Relaciones:

- Un usuario tiene un carrito (1:1)
- Un carrito tiene muchos productos (1:N)
- Un usuario puede tener muchas órdenes (1:N)
- Una orden tiene un pago (1:1)

**7. Modelo No Relacional**

Colección: orders

{
"orderId": 1,
"user": {
"id": 1,
"name": "Dana"
},
"products": [
{
"name": "Zapatos",
"quantity": 2,
"price": 120000
}
],
"total": 240000,
"status": "PAID"
}

**8. Autenticación**

Se utiliza JWT (JSON Web Token) para la autenticación de usuarios.

Cuando el usuario inicia sesión, el sistema genera un token que es enviado en cada petición posterior para validar su identidad.

Esto permite que el sistema sea stateless y escalable.

**9. Seguridad**

Se utiliza HTTPS mediante TLS para proteger la comunicación entre el cliente y el servidor.

Esto permite cifrar la información enviada, evitando ataques como robo de credenciales o interceptación de datos.

**10. CORS**

CORS (Cross-Origin Resource Sharing) permite que el frontend pueda comunicarse con el backend aunque estén en diferentes dominios.

Esto es necesario en aplicaciones web modernas donde el cliente y el servidor están separados.

## PARTE PRÁCTICA
