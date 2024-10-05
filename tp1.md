                            file.c 
sysfile.c -> syslseek() -> filelseek() return0;

int -> trappe d'appel système (provoque une exception)
chercher argument 

Question 1

Question 2
1 - macro qui génère du code assembleur
    SYSCALL(lseek) -> .globl lseek
                exporté à l'exterieur du fichier
        lseek: movl $SYS_## lseek
                    prends deux symboles S1 et S2 et génère s1s2 -> SYS_ ## lseek = SYS_lseek, %eax

                    on charge dans eax 22 le numéro de l'appel système
            int 64
            ret

devient une fonction utilisateur (ceci ne fait pas partie du noyau)

pas de errno qui indique la raison de l'erreur
seul l'utilisateur peut modifier errno et a connaissance de son existence (donc lseek utilisateur)

en plus de renvoyer uen valeur dans registre %eax devrait renvoyer errno dans un autre registre et en revenant de la primitive syteme alors on prends la valeur mise dans %ebx et on la met dans la variable utilisateur

2 - y a pas de prototype de lseek, on construit un faux prototype pour le compilateur car il existe une fonction assembleur mais pas de fonction.c

types a utiliser dans le prototype

pourquoi _testlseek\

_ pour eviter de confondre avec commande du système natif et pas qu'on garde par mégarde une commande xv6 sur linux