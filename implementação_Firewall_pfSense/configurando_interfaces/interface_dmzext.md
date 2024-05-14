<h1>Interface DMZEXT</h1>
    
   **Configurando o WAF**
    
   Crie uma nova máquina virtual com a .iso Debian, nesse projeto está com o nome **WAF_machine**, e siga as orientações dessas documentações para instalar o Nginx ModSecurity: 
    
   [NGINX ModSecurity WAF](https://docs.nginx.com/nginx-waf/)
    
   [How to Install ModSecurity for Nginx on Debian/Ubuntu](https://www.tecmint.com/install-modsecurity-nginx-debian-ubuntu/)
    
   **Configure a rede na DMZEXT:**
<div align="center">
  <img src="https://github.com/biancagomesalves/projeto_2_rede_firewall_WAF_SIEM/blob/a622bf803f6908b4aac03f16e98901337a3ef49c/imagens/configurando_interfaces/iface_dmzext.png" width="70%"/>
</div>

   **Ligue a máquina e atribua um IP com essas instruções:**
    
   No terminal, abre o arquivo de configuração do Nginx com o seguinte comando: 
    
   ```bash
   nano /etc/nginx/nginx.conf
   ```
<div align="center">
   <img src="https://github.com/biancagomesalves/projeto_2_rede_firewall_WAF_SIEM/blob/9c8a2fce0ea0a40f756d457b62012df8f222ee12/imagens/configurando_interfaces/iface_dmzext01.png" width="70%"/>
</div>

   **Para enviar os logs do WAF ao Graylog, configurar esse arquivo com os seguintes dados:** 
<div align="center">
  <img src="https://github.com/biancagomesalves/projeto_2_rede_firewall_WAF_SIEM/blob/9c8a2fce0ea0a40f756d457b62012df8f222ee12/imagens/configurando_interfaces/iface_dmzext02.png" width="70%"/>
    
</div>
   Informando o endereço <b>IP do Graylog</b> com a <b>porta</b> padão <b>UDP 1514</b>.
    
   Salve o arquivo com **CRTL + 0**. 
   
   No terminal digite o comando: 
    
   ```bash
   nginx -t #verifica se a sintaxe está correta
   nginx -s realod #recarrega as configurações do nginx
   ```
    
   <aside>
    💡 O WAF e o Graylog estão em DMZs diferentes, sendo assim o firewall bloqueia o tráfego, e não é possível enviar os logs apenas com essa configuração, nesse caso é necessário criar uma regra no firewall.
   </aside>
    
   ---
  
   No menu: 
    
   **Firewall ➡️ [Rules](http://192.168.56.2/firewall_rules.php) ➡️ [DMZEXT](http://192.168.56.2/firewall_rules.php?if=opt2)**
    
   **Configure a regras para liberar o acesso do WAF ao Graylog, para enviar os logs através do protocolo UDP:** 
<div align="center">
   <img src="https://github.com/biancagomesalves/projeto_2_rede_firewall_WAF_SIEM/blob/a622bf803f6908b4aac03f16e98901337a3ef49c/imagens/configurando_interfaces/iface_dmzext03.png" width="70%"/>
  
 <img src="https://github.com/biancagomesalves/projeto_2_rede_firewall_WAF_SIEM/blob/a622bf803f6908b4aac03f16e98901337a3ef49c/imagens/configurando_interfaces/iface_dmzext04.png" width="70%"/>
</div>
   **Salve e aplique as mudanças.**
  
   ---
   
   Na prática o sevidor não está hospedado, porém é possível simular o acesso para ver o envio dos logs do WAF para o Graylog, pois ele está na linha de frente da rede, recebendo todas as requisições de origem da internet/clientes. Mas a rede ainda não reconhece o IP do WAF sendo assim deve ser criado um IP virtual e realizar o NAT. 
   
   ![Criando IP virtual e realizando NAT - WAF](https://github.com/biancagomesalves/projeto_2_rede_firewall_WAF_SIEM/blob/cfd3f01e4cbc7d5e6cfd95fb47af2c14535d0b3b/implementa%C3%A7%C3%A3o_Firewall_pfSense/Criando%20IP%20virtual%20e%20realizando%20NAT%20-%20WAF.md)
    
**Verificando os logs no Graylog enviados pelo WAF:**
 <div align="center">   
 <img src="https://github.com/biancagomesalves/projeto_2_rede_firewall_WAF_SIEM/blob/a622bf803f6908b4aac03f16e98901337a3ef49c/imagens/configurando_interfaces/iface_dmzext06.png" width="70%"/>
 </div>
   **Para implementar mais segurança a rede, é necessário o uso de um IDS/IPS para detectar tráfego malicioso e realizar ações de bloqueio, pois somente o WAF não oferece uma proteção abrangente.**
   ---
   <h2>Regra para autotizar conexão do WAF com o servidor web</h2>

   Crie a regra conforme especificações: 
   
       Sendo Source IP = IP do WAF 
       
       Destination IP = IP do Servidor Web
       Port 80 - para o tráfego HTTP
<div align="center"> 
<img src="https://github.com/biancagomesalves/projeto_2_rede_firewall_WAF_SIEM/blob/3ef0ec245a3809498f25186b830e3bc8fe017f4c/imagens/configurando_interfaces/iface_dmzext07.png" width="70%"/>
</div>

   
