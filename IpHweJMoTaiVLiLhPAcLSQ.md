# stdin,stdoutリダイレクト
###### tags: `c-lang`
@6H8pvZw8SZGVQ5E4AmpM_A 


## stdinをパイプにリダイレクト
```shell
$mkfifo mystdin
```

```clike=
#include<stdio.h>
#include<stdlib.h>
#include<sys/types.h>
#include<sys/wait.h>
#include<unistd.h>
#include<fcntl.h>
#include<errno.h>
char *cmd = "/challenge/embryoio_level117";
const char* file = "mystdin";
const char* stdoutfile = "mystdout";
// const char* cd2 = "/tmp/ucxfie";
// char cwd[256];
const char* argv[1] = {"ioxprq"};
int pwncollege() {
	int fd = open(file,O_RDWR);
	//dup2(fd,315);
	//dup2(315,0);
	freopen(file,"r",stdin);
	//freopen(stdoutfile,"w",stdout);
	execve(cmd,argv,NULL);
}
int main(int argc,char *argv[],char *envp[]){
	pid_t p;
	pid_t child = fork();
	if(child == -1){
		printf("fork failed\n");
		return 1;
	}else if (!child){
		pwncollege();
		return 127;
	}

	do {
		int status = 0;
		p = waitpid(child,&status,0);
		if(p == -1)
			break;
	}while(p != child);

	return 0;
}
hacke
    ```