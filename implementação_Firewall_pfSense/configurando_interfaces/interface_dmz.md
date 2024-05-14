 

<h1>Interface DMZ</h1>
    <h2>Regra para autorizar ICMP(ping)</h2>
   No menu, navegue até a interface da DMZ, pois é necessário a configuração de regras para autorizar o tráfego nesta interface. Neste projeto é criado a regra de autorização de ping na DMZ. 
    
   **Firewall ➡️ [Rules](http://192.168.56.10/firewall_rules.php) ➡️ [DMZ](http://192.168.56.10/firewall_rules.php?if=opt1) ➡️ [Edit](http://192.168.56.10/firewall_rules_edit.php?if=opt1&after=-1)**
    
   Adicione uma regra de **Pass ping** acima da regra já existente “Deny By Default”, com as seguintes especificações:
    
   <img src="https://github.com/biancagomesalves/projeto_2_rede_firewall_WAF_SIEM/blob/cf7d2f2de592fe6a7a64e39340326865bb8d0a20/imagens/configurando_interfaces/iface_dmz01.png" width="70%"/>
    
   <aside>
    💡 Obs. O protocolo autorizado é o ICMP (usado aqui para teste de conexão - ping), foi liberado somente os types (ECHO request e o ECHO replay). Após essa configuração, caso queira testar se a regra está funcionando, acesse a máquina virtual do servidor <b>Server_Web</b>, faça o login com as credenciais que você criou e em seguida realize o seguinte comando no terminal:
    
   </aside>
    
   ```bash
   ping 172.16.10.1 #ip da interface DMZ
   ```

    
   **Verifique o resultado do ping com sucesso:**
    
   ![iface_dmz02](https://github.com/biancagomesalves/projeto_2_rede_firewall_WAF_SIEM/blob/cf7d2f2de592fe6a7a64e39340326865bb8d0a20/imagens/configurando_interfaces/iface_dmz02.png)
    
<h2>Regra para autorizar host da DMZ realizarem atualização</h2>
Configurar uma regra no firewall para que as máquinas tenha acesso à internet e possam ser atualizadas:

   <img src="https://github.com/biancagomesalves/projeto_2_rede_firewall_WAF_SIEM/blob/0196fc145cd3f01afc75cb2f6ac5f662d59a712f/imagens/configurando_interfaces/iface_dmz03.png" width="70%"/>

   Clique em **Save e aplique as alterações.** 
