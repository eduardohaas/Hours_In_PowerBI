<h1 align="center">English</h1>

To work with hours in DAX, we face some difficulties, but it is possible to work using decimal conversion.

To do so, we must follow the following steps:

Load the dataset and create a column that calculates the difference between the desired periods.
Example: ```ruby
Diff = Records[Departure_DateTime] - Records[Entry_DateTime]
```

Next, we need to convert this column to decimal by multiplying the column by 24.
Example: 
```ruby
Decimal = Records[Diff] * 24
```

Then, we start taking measurements. First, we calculate the sum of these decimal values.
Example: 
```ruby
01_Total_Hours_(Decimal) = SUM(Records[Decimal])
```

Having these values, we need to use the following measure that converts this decimal to the H.H.T. format.
Example:
```ruby
02_Convert_Hours (hh:mm:ss) =
VAR vDecimalHours = [01_Total_Hours_(Decimal)]
VAR vHours =
    INT ( vDecimalHours )
VAR vDecimalMinutes = 60 * ( vDecimalHours - vHours )
VAR vMinutes =
    INT ( vDecimalMinutes )
VAR vSeconds =
    ROUND ( 60 * ( vDecimalMinutes - vMinutes ), 0 )
VAR vHH =
    IF ( LEN ( vHours ) = 1, "0" & vHours, vHours )
VAR vMM =
    IF ( LEN ( vMinutes ) = 1, "0" & vMinutes, vMinutes )
VAR vSS =
    IF ( LEN ( vSeconds ) = 1, "0" & vSeconds, vSeconds )
VAR vResult = vHH & ":" & vMM & ":" & vSS
RETURN
    CONVERT ( vHH & vMM & vSS, INTEGER )
```
Remember to change the format of the upper part to 00:00:00
![image](https://github.com/eduardohaas/Hours_In_PowerBI/assets/84861180/40322295-b069-4037-82cd-992b8f1eb98f)

Then we will have the result
![image](https://github.com/eduardohaas/Hours_In_PowerBI/assets/84861180/563843e3-9334-4aef-bff0-37a856eaa000)

<h1 align="center">Português</h1>

Para tabalhar com horas em dax, temos algumas dificuldades, porem é possivel trabalhar utilizando a conversão de decimais. 

Para fazer devemos seguir os seguintes passos: 

Carregar o Data_SET e criar uma coluna que realize a diferença entra o periodo desejado
Exemplo: 
```ruby
Dif = Registros[Data_Hora_Saida]-Registros[Data_Hora_Entrada]
```

Porterior devemos converter esta coluna para decimal realizando a multiplicação da coluna por 24 
Exemplo : 
```ruby
Decimal = Registros[Dif]*24
```

Posterior começamos a realizar as medidas, primeiro realizamos a soma destes valores decimais
Exemplo: 
```ruby
01_Total_Horas_(Decimal) = SUM(Registros[Decimal])
```

Tendo estes valores, precisamos utilizar a seguinte medida que realiza a conversão deste decimal para o modelo H.H.T.
Exemplo: 
```ruby
02_Convert_Horas (hh:mm:ss) =
VAR vHorasDecimal = [01_Total_Horas_(Decimal)]
VAR vHoras =
    INT ( vHorasDecimal )
VAR vMinutosDecimal = 60 * ( vHorasDecimal - vHoras )
VAR vMinutos =
    INT ( vMinutosDecimal )
VAR vSegundos =
    ROUND ( 60 * ( vMinutosDecimal - vMinutos ), 0 )
VAR vHH =
    IF ( LEN ( vHoras ) = 1, "0" & vHoras, vHoras )
VAR vMM =
    IF ( LEN ( vMinutos ) = 1, "0" & vMinutos, vMinutos )
VAR vSS =
    IF ( LEN ( vSegundos ) = 1, "0" & vSegundos, vSegundos )
VAR vResultado = vHH & ":" & vMM & ":" & vSS
RETURN
    CONVERT ( vHh & vMm & vSS, INTEGER )
```

Lembre-se de Muda o formato da parte superior para 00:00:00
![image](https://github.com/eduardohaas/Hours_In_PowerBI/assets/84861180/40322295-b069-4037-82cd-992b8f1eb98f)

Posterior Teremos o resultado
![image](https://github.com/eduardohaas/Hours_In_PowerBI/assets/84861180/563843e3-9334-4aef-bff0-37a856eaa000)

