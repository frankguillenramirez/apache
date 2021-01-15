# apache


  
 - name: Descargando el paquete
      copy:
        src: http://10.78.11.226:8415/FlexPos/paquetes/cambia_pass.sh
        dest: /tmp/
        remote_src: yes

  - name: Validando si el programa esta instalado en las cajas
      shell: "for i in $(cat /etc/hosts | grep 'REG' | awk '{print $1}');do if ssh -q -o ConnectTimeout=1 $i 'echo -n 2>&1'; [ $? -eq 255 ]; then echo $i sin conexion; else scp files/usuarios_flex.csv root@$i:/tmp; scp files/cambia_pass.sh root@$i:/tmp; ssh $i \"sh /tmp/cambia_pass.sh\"; fi; done" 
      register: caja  
