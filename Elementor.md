# Elementor

## Validacion de campos de formulario de acuerdo a los requerimientos.

Ejemplo para la validacion de los campos de formulario:

1. En el espacio número celular un número de 10 caracteres que inicie con el número 3, sino le debe mostrar error y no permitirle enviar la información.
2. En el espacio nombre asegurar que mínimo escriba 5 caracteres,  sino le debe mostrar error y no permitirle enviar la información.


Se agrega el siguiente codigo php en: Hello Elementor Child: functions.php

## Codigo php insertado

```
// Agregado por Arturo

// Valida los caracteres del campo nombre
add_action( 'elementor_pro/forms/validation/text', function( $field, $record, $ajax_handler ) {

	// restringe la cantidad para que sea mayor o igual a 4 caracteres en el campo nombre

    if( 4 >= strlen(trim($field['value'])) ){
       $ajax_handler->add_error( $field['id'], 'Tu nombre debe tener al menos 5 caracteres.' );
    }
}, 10, 3 );

// Valide que el campo Tel esté en formato de 10 digitos.
add_action( 'elementor_pro/forms/validation/tel', function( $field, $record, $ajax_handler ) {

    // Haga coincidir este formato 1234567890

    if ( preg_match( '/[0-9]{10}/', $field['value'] ) !== 1 ) {
        $ajax_handler->add_error( $field['id'], 'Por favor ingresa un numero de celular valido ej: 3209876543' );
    }
}, 10, 3 );

// Fin del codigo agregado por arturo
```
