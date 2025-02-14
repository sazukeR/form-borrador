## 1. Instalar Reach Hook Form

```
npm i react-hook-form
```

## 2. Acceder al hook dentro del componente

```
export const App = () => {....
 const {} = useForm()
```

## 3. Registrar campos del formulario

```
export const App = () => {....
 const { register } = useForm()


return (....

     <input
      type="text"
      name="nombre"
      {...register("nombre")}
     />
```

## 4. Manejar el envio de formulario

```
export const App = () => {....
 const { register, handleSubmit } = useForm();

 const onSubmit = handleSubmit((data) => {
  console.log(data);
 });

return (....

  <form onSubmit={onSubmit}>
    <>campos del formulario....</>
    <button type="submit">Enviar</button>
  </form>
```

## 5. Crear validaciones para los inputs

```
   <form onSubmit={onSubmit}>
    <div>
     <label>Nombre:</label>
     <input
      type="text"
      name="nombre"


      {...register("nombre", {
       required: {
        value: true,
        message: "Nombre es requerido",
       },
       maxLength: 20,
       minLength: 2,
      })}


     />
   </form>
```

## 5. Utilizar formState para visualizar el estado actual del formulario y hacer validaciones

- con formState podemos capturar errores

```
export const App = () => {...

 const {
  register,
  handleSubmit,
  formState: { errors },
 } = useForm();

  return......

   <form onSubmit={onSubmit}>
    <div>
     <label>Nombre:</label>
     <input
      type="text"
      name="nombre"


      {...register("nombre", {
       required: {
        value: true,
        message: "Nombre es requerido",
       },
       maxLength: 20,
       minLength: 2,
      })}

     />
    {errors.nombre?.type === "required" && <span>Nombre requerido</span>}
     {errors.nombre?.type === "maxLength" && (
      <span>Nombre no debe ser mayor a 20 caracteres</span>
     )}


   </form>
```

## 6. Utilizar watch para ver el estado actual de todo el formulario

- podemos mostrar el estado actual del formulario en el html, para controlar el estado del mismo mientras estamos en desarrollo.

```

export const App = () => {...

 const {
  register,
  handleSubmit,
  formState: { errors },
  watch
 } = useForm();

return...

  <form onSubmit={onSubmit}>
    <>campos del formulario....</>

    <pre style={{ width: "400px" }}>{JSON.stringify(watch(), null, 2)}</pre>
  </form>
```
