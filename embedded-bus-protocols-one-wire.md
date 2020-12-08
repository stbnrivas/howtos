# 1wire

Creado por Dallas Semiconductor, originalmente llamado MicroLAN es un protocolo es half-duplex y el maestro debe iniciar la transmision. bus de comunicacion 1 wire aka DQ o OWIO. la resistencia PULL-UP conecta la linea de datos a +5V en caso de que no haya transmision la linea permanece en HIGH (estado iddle)


4 basic operations

- reset
- write 0 (to slaves)
- write 1 (to slaves)
- read    (from slaves)


write operation:

the master start condition from 1 to 0
all write should keep a minimun of 60 us with a minimun of 1 us between cicles of writing
the slave read after 16-60 us after start condition


read operation:

the master put a start condition
the time to read start after
line should be to keep in low for a minimoun of 1 us