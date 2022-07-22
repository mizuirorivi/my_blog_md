# forkして子プロセス実行
@6H8pvZw8SZGVQ5E4AmpM_A 
###### tags: `c-lang`

```c=
#include<stdio.h>
#include<stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

void pwncollege(char *argv[],char *envp[]){
    execve("/challenge/embryoio_level29",argv,envp);
}
int main(int argc,char *argv[],char *envp[]){
    pid_t pid,child,p;
    int status;
    int ret;

    child = fork();
    if(child == (pid_t)-1){
        printf("fork failed!!\n");
        return 1;
    }else if(!child){
            pwncollege(argv,envp);
        
        return 127;
    }

    do {
        status = 0;
        p = waitpid(child, &status, 0);
        if (p == (pid_t)-1)
            break; /* Error */
    } while (p != child);

    return 0;
}
```

# 環境変数指定
```c=
#include<stdio.h>
#include<stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

char *array[10] = {"/challenge/embryoio_level33","fkrnxhdvnc"};
char *env[10] = {"mgmwel=wsknikdvdr"};
void pwncollege(char *argv[],char *envp[]){
    execve("/challenge/embryoio_level33",array,env);
}
int main(int argc,char *argv[],char *envp[]){
    pid_t pid,child,p;
    int status;
    int ret;
    
    child = fork();
    if(child == (pid_t)-1){
        printf("fork failed!!\n");
        return 1;
    }else if(!child){
            pwncollege(argv,envp);
        
        return 127;
    }

    do {
        status = 0;
        p = waitpid(child, &status, 0);
        if (p == (pid_t)-1)
            break; /* Error */
    } while (p != child);

    return 0;
}
```

## stdinからリダイレクト
```c=
#include<stdio.h>
#include<stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
#include <fcntl.h>

const char* file = "/tmp/upqpfz";
char *array[10] = {"/challenge/embryoio_level33","fkrnxhdvnc"};
char *env[10] = {"mgmwel=wsknikdvdr"};

void pwncollege(char *argv[],char *envp[]){
    int fd = open(file, O_RDWR | O_CREAT, S_IRUSR | S_IWUSR);
    dup2(fd,0);
    execve("/challenge/embryoio_level33",array,env);
}
int main(int argc,char *argv[],char *envp[]){
    pid_t pid,child,p;
    int status;
    int ret;
    
    child = fork();
    if(child == (pid_t)-1){
        printf("fork failed!!\n");
        return 1;
    }else if(!child){
            pwncollege(argv,envp);
        
        return 127;
    }

    do {
        status = 0;
        p = waitpid(child, &status, 0);
        if (p == (pid_t)-1)
            break; /* Error */
    } while (p != child);

    return 0;
}
```

## 環境変数を空にして実行
```c=
#include<stdio.h>
#include<stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
#include <fcntl.h>

char *array[10] = {"/bin/env","-i","/challenge/embryoio_level35"};

void pwncollege(char *argv[],char *envp[]){
    execve("/challenge/embryoio_level35",array,NULL);
}
int main(int argc,char *argv[],char *envp[]){
    pid_t pid,child,p;
    int status;
    int ret;
    
    child = fork();
    if(child == (pid_t)-1){
        printf("fork failed!!\n");
        return 1;
    }else if(!child){
            pwncollege(argv,envp);
        
        return 127;
    }

    do {
        status = 0;
        p = waitpid(child, &status, 0);
        if (p == (pid_t)-1)
            break; /* Error */
    } while (p != child);

    return 0;
}
```