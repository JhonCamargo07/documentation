# Alertas sweetalert

```js
npm install sweetalert2
```

```js
<script src="//cdn.jsdelivr.net/npm/sweetalert2@11"></script>
```

Login
```javascript
 alertaFlotante('Error en los datos', 'No se encontró ningún registro que coincida con las credenciales', '#f27474', 'error');
```

Algunas funciones

```JS
let alertaFlotante = (titulo, texto, colorBoton, imagen) => {
    swal.fire({
        title: `${titulo}`,
        text: `${texto}`,
        confirmButtonText: 'Ok, entendí',
        confirmButtonColor: `${colorBoton}`,
        // imageUrl: `${imagen}`,
        // imageWidth: "auto",
        // imageHeight: 135,
        icon: `${imagen}`,
        timer: 5090,
        timerProgressBar: true,
        didOpen: (toast) => {
            toast.addEventListener('mouseenter', Swal.stopTimer)
            toast.addEventListener('mouseleave', Swal.resumeTimer)
        },
        showClass: {
            popup: 'animate__animated animate__fadeInDown'
        },
        hideClass: {
            popup: 'animate__animated animate__fadeOutUp'
        },
        allowOutsideClick: false,
        allowEscapeKey: false,
        allowEnterKey: false,
        stopKeydownPropagation: false,
    });
}
let alertaConFormulario = (titulo, texto, textBtn, colorBoton, imagen) => {
    swal.fire({
        title: `${titulo}`,
        text: `${texto}`,
        confirmButtonText: `${textBtn}`,
        confirmButtonColor: `${colorBoton}`,
        showCancelButton: true,
        cancelButtonText: 'Cancelar',
        // imageUrl: `${imagen}`,
        // imageWidth: "auto",
        // imageHeight: 135,
        icon: `${imagen}`,
        showClass: {
            popup: 'animate__animated animate__fadeInDown'
        },
        hideClass: {
            popup: 'animate__animated animate__fadeOutUp'
        },
    }).then((result) => {
        if (result.isConfirmed) {
            alertaDiminuta('success', 'Usuario actualizado correctamente');
        }
    })
}
let alertaFlotanteConRedirecion = (titulo, texto, colorBoton, imagen, direccion) => {
    swal.fire({
        title: `${titulo}`,
        text: `${texto}`,
        confirmButtonText: 'Ok, entendí',
        confirmButtonColor: `${colorBoton}`,
        imageUrl: `${imagen}`,
        imageWidth: "auto",
        imageHeight: 135,
        timer: 5090,
        timerProgressBar: true,
        didOpen: (toast) => {
            toast.addEventListener('mouseenter', Swal.stopTimer)
            toast.addEventListener('mouseleave', Swal.resumeTimer)
        },
        showClass: {
            popup: 'animate__animated animate__fadeInDown'
        },
        hideClass: {
            popup: 'animate__animated animate__fadeOutUp'
        },
        allowOutsideClick: false,
        allowEscapeKey: false,
        allowEnterKey: false,
        stopKeydownPropagation: false,
    }).then((result) => {
        if (result.isConfirmed) {
            location.href = `${direccion}`;
        }
    });
    // Redirecionar
    setInterval(() => {
        location.href = `${direccion}`;
    }, 5100);
}

let alertaDiminuta = (icon, title) => {
    swal.fire({
        icon: `${icon}`,
        title: `${title}`,
        toast: true,
        position: 'top-end',
        showConfirmButton: false,
        timer: 3000,
        timerProgressBar: true,
        didOpen: (toast) => {
            toast.addEventListener('mouseenter', Swal.stopTimer)
            toast.addEventListener('mouseleave', Swal.resumeTimer)
        }
    })
}

```

Ejemplo de confirmacion
```js
Swal.fire({
  title: "Are you sure?",
  text: "You won't be able to revert this!",
  icon: "warning",
  showCancelButton: true,
  confirmButtonColor: "#3085d6",
  cancelButtonColor: "#d33",
  confirmButtonText: "Yes, delete it!",
}).then((result) => {
  if (result.isConfirmed) {
    Swal.fire("Deleted!", "Your file has been deleted.", "success");
  }
});
```

Por: [Jhon Camargo](http://jhoncamargo.000webhostapp.com/)