#define _GNU_SOURCE
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
  char *line = NULL;
  size_t len = 0;

  while (1) {
    printf("Enter programs to run.\n");
    printf("> ");
    if (getline(&line, &len, stdin) == -1) {
      break;
    }
    line[strcspn(line, "\n")] = '\0';

    pid_t pid = fork();
    if (pid == 0) {
      if (execl(line, line, (char *)NULL) == -1) {
        printf("Exec failure\n");
        exit(1);
      }
    } else if (pid > 0) {
      waitpid(pid, NULL, 0);
    } else {
      perror("fork failure");
    }
  }
  free(line);
  return 0;
}
