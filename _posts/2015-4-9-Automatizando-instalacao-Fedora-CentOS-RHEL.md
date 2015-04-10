---
layout: post
title: Automatizando instalação Fedora/CentOS/RHEL
---

Cada vez que formatamos nosso notebook de trabalho, geralmente usamos exatamente os mesmos critérios de instalação como usuários, configurações de disco, rede, seleção de pacotes e tudo mais. Em um servidor isso vai inclusive bem além.

Se você ainda não conhece, vale a pena dar uma olhada no [Kickstart](https://github.com/rhinstaller/pykickstart/blob/master/docs/kickstart_docs.rst) que é uma instalação baseada em script do [Anaconda](https://fedoraproject.org/wiki/Anaconda). 

Já percebeu que toda vez que você instala o Fedora/CentOS/RHEL um arquivo chamado anaconda-ks.cfg aparece no /root?! Esse arquivo guarda todas as configurações que você fez durante o processo de instalação no modo gráfico Anaconda. Ou seja, em uma instalação futura em vez de você fazer todo processo manual novamente, você simplesmente vai informar que a instalação deve seguir essas configurações desse arquivo que vai estar geralmente em outra máquina (eu por exemplo tenho no meu github, lembrando que as senhas são criptografadas).

O processo é simples, quando você inicializa a imagem do sistema operacional baseado no Anaconda, vai aparecer a opção "Instalar sistema XXX" você vai manter ela selecionada e acessar as opções avançadas pressionando a tecla TAB. A instrução que deve aparecer é responsável por carregar a instalação, basta incluir ao final um espaço em branco e a chave/valor de acordo com a sintaxe "ks=http://server/arquivo.cfg", por exemplo:

Antes:
> vmlinuz initrd=initrd.img inst.stage2=hd:LABEL=Fedora-22_B-x86_64 quiet

Depois:
> vmlinuz initrd=initrd.img inst.stage2=hd:LABEL=Fedora-22_B-x86_64 quiet ks=http://200.1.2.3/f22-ks.cfg

Isso é muito útil não apenas para poupar o seu tempo, mas também para evitar erros durante o processo. Caso precise criar o arquivo manualmente, [acesse a documentação para mais informações](https://github.com/rhinstaller/pykickstart/blob/master/docs/kickstart_docs.rst).
