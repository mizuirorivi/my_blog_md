# c-lang Tip集
###### tags: `c-lang`


### forkしないと、親プロセスが引き継がれるのでプロセスの上書きがされない？
```c=
#include<stdio.h>
#include<stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
#include <fcntl.h>

char *array[1] = {"/tmp/qgacnd"};
char *cmd = "/challenge/embryoio_level88";
// const char* file = "nybmce";
// const char* cd2 = "/tmp/ucxfie";
// char cwd[256];

void pwncollege(char *argv[],char *envp[]){
    printf("######################################\n");
    printf("[+] pwn colledge start\n");

    // if (!chdir(cd2))
    //     printf("[!]change current directory failed\n");
    // if(getcwd(cwd, sizeof(cwd)) == NULL)
    //     printf("[!]get current directory failed!!\n");
    
    // printf("current directory: %s",cwd);

    // int fd = open(file, O_RDWR | O_CREAT, S_IRUSR | S_IWUSR);
    // dup2(fd,0);
    execve(cmd,array,NULL);
}
int main(int argc,char *argv[],char *envp[]){
    pwncollege(argv,envp);
}
```

```bash
bash -c ~/solve
```

ここで、solveを実行する時にbashというプロセスで認識される

```
hacker@embryoio_level88:~$ bash ~/my_script.sh 
######################################
[+] pwn colledge start
[INFO] This challenge will now perform a bunch of checks.
[INFO] If you pass these checks, you will receive the flag.
[TEST] Performing checks on the parent process of this process.
[TEST] Checking to make sure the process is a non-interactive shell script.
[GOOD] You have passed the checks on the parent process!
[TEST] My argv[0] should have a value of /tmp/qgacnd! Let's check...
[HINT] argv[0] is passed into the execve() system call *separately* from the program path to execute.
[HINT] This means that it does not have to be the same as the program path, and that you can actually
[HINT] control it. This is done differently for different methods of execution. For example, in C, you
[HINT] simply need to pass in a different argv[0]. Bash has several ways to do it, but one way is to
[HINT] use a combination of a symbolic link (e.g., the `ln -s` command) and the PATH environment variable.
[GOOD] You successfully passed the argument value check!
[GOOD] Success! You have satisfied all execution requirements. Here is your flag:
pwn.college{cHxLAHzmHfDnDA3wNAn2tPhM4tx.dhDOsITN0QzW}
```
> pwncolldge embryoio_level88