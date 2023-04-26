#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#include <unistd.h>
/***************************************/

#define _LINE_LENGTH 64
/***************************************/

/***************************************/
char *bash(const char *cmd)
{
  char shit[_LINE_LENGTH];
  char *fuck = (char *)malloc(0);
  FILE *file = popen(cmd, "r");
  if (NULL == file)
    return fuck;
  uint8_t i = 2;
  while (read(fileno(file), shit, sizeof shit - 1) > 0)
  {
    fuck = realloc(fuck, _LINE_LENGTH * i * sizeof(char));
    strncat(fuck, shit, strlen(shit));
    i++;
  }
  pclose(file);
  // printf("read_len=%ld\n", strlen(shit));
  // printf("shit=%s\n", shit);
  return fuck;
}

int main(void)
{
  char *cmd = "uname -a";
  char *cmd2 = "df -h";
  char *result = bash(cmd);
  char *result2 = bash(cmd2);
  printf("result = %s\n", result);
  printf("result2 = %s\n", result2);

  return 0;
}
