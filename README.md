neste repositorio utilizo a ferramenta medusa a fim des estudos pela plataforma DIO.

http://foofus.net/goons/jmk/medusa/medusa.html


E possivel fazer ataques em varios protocolos com ssh, smb e ate mesmo a formularios WEB

1- Ataque de Força Bruta em SSH
O módulo ssh é um dos mais comuns. Você pode testar um único usuário contra uma lista de senhas ou usar listas para ambos.
Exemplo com usuário único: medusa -h 10.0.2.15 -u admin -P /caminho/senhas.txt -M ssh
Exemplo com listas de usuários e senhas: medusa -h 172.16.45.129 -U usuarios.txt -P senhas.txt -M ssh -n 22
Explicação dos parâmetros:
-h: Define o IP ou hostname do alvo
.
-u / -U: Usuário único ou arquivo com lista de usuários
.
-p / -P: Senha única ou arquivo com lista de senhas
.
-M: Especifica o módulo (neste caso, ssh)
.
-n: Porta do protocolo (opcional se for a padrão)


2- Ataque de Força Bruta em SMB (Windows/Rede)
Para o serviço SMB, a Medusa utiliza o módulo smbnt. Este ataque é útil para tentar acessar compartilhamentos de rede ou contas de administrador em máquinas Windows
.
Exemplo básico: medusa -h 192.168.1.20 -u administrator -P senhas.txt -M smbnt
Exemplo com verificação de senha em branco ou igual ao usuário: medusa -h 192.168.1.20 -u administrator -P senhas.txt -M smbnt -e ns
Parâmetros adicionais:
-e ns: Instrução para verificar adicionalmente se a conta possui senha em branco (n) ou se a senha é igual ao nome de usuário




3 - Ataque a Formulários Web
O ataque a formulários web é mais complexo, pois exige o uso do módulo web-form e parâmetros específicos para identificar como o formulário envia os dados e qual mensagem indica erro
.
Exemplo de comando: medusa -h 127.0.0.1 -u admin -P wordlist.txt -M web-form -m FORM:"admin/login.php" -m DENY-SIGNAL:"Login incorreto" -m FORM-DATA:"post?user=&pass=&Login=Login"
Explicação dos parâmetros de módulo (-m):
FORM: O caminho relativo para a página de processamento do formulário no servidor
.
DENY-SIGNAL: A mensagem de erro que o site exibe quando o login falha. A Medusa usa isso para saber que deve continuar tentando
.
FORM-DATA: Define como os dados são enviados (ex: via POST ou GET) e mapeia onde o usuário e a senha devem ser inseridos na requisição (geralmente onde os campos ficam vazios após o = )

