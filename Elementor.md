# Elementor

## Validacion de campos de formulario de acuerdo a los requerimientos.

Ejemplo para la validacion de los campos de formulario:

1. En el espacio número celular se asegure que el aspirante deja un número de 10 caracteres que inicie con el número 3, sino le debe mostrar error y no permitirle enviar la información.
2. En el espacio correo electrónico, no permitirle al aspirante correos con dominio midominio.com, sino le debe mostrar error y no permitirle enviar la información.
3. En el espacio nombre asegurar que mínimo el aspirante escriba 5 caracteres, sino le debe mostrar error y no permitirle enviar la información.

Se agrega el siguiente codigo php en: Hello Elementor Child: functions.php cambiando la informacion del dominio.

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
add_action( 'elementor_pro/forms/validation/tel', function( $field, $record, $ajax_handler, $minDigits = 9, $maxDigits = 9 ) {

    // Haga coincidir este formato 1234567890, que inicie con el numero "3" y que su longitud sea 10 caracteres

    if ( preg_match('/^[3][0-9]{'.$minDigits.','.$maxDigits.'}\z/', $field['value'] ) !== 1 ) {
        $ajax_handler->add_error( $field['id'], 'Por favor ingresa un numero de celular valido ej: 3400298930' );
    }
}, 10, 3 );

// Evita correos corporativos.
add_action( 'elementor_pro/forms/validation/email', function( $field, $record, $ajax_handler ) {

	// Lista negra de dominios
	$black_list_domains = [
		'midominio.com',
	];

	$email_domain = explode( '@', $field['value'] )[1];

	if ( in_array( $email_domain, $black_list_domains ) ) {
		$ajax_handler->add_error( $field['id'], 'Lo sentimos, correos como ' . $email_domain . ' no están permitidos, intenta usar tu correo personal.' );
		return;
	}
}, 10, 3 );

// Fin del codigo agregado por arturo
```
