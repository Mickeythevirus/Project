# Project
file handling










#include <stdio.h>
#include <stdlib.h>

int main() {
    FILE *inputFile, *outputFile;
    char fileName[50];
    char ch;
    long fileSize;
    long i;

    // Get the name of the file to read
    printf("Enter the name of the file to read: ");
    scanf("%s", fileName);

    // Open the file for reading
    inputFile = fopen(fileName, "r");
    if (inputFile == NULL) {
        printf("Error opening file!\n");
        exit(1);
    }

    // Get the size of the file
    fseek(inputFile, 0, SEEK_END);
    fileSize = ftell(inputFile);

    // Allocate memory to store the contents of the file
    char *fileContents = (char *)malloc(fileSize * sizeof(char));

    // Read the file contents into the memory
    fseek(inputFile, 0, SEEK_SET);
    fread(fileContents, sizeof(char), fileSize, inputFile);

    // Close the input file
    fclose(inputFile);

    // Open the file for writing
    outputFile = fopen("output.txt", "w");
    if (outputFile == NULL) {
        printf("Error opening file!\n");
        exit(1);
    }

    // Write the contents of the file in reverse order to the output file
    for (i = fileSize - 1; i >= 0; i--) {
        fputc(fileContents[i], outputFile);
    }

    // Close the output file
    fclose(outputFile);

    // Display the contents of the file in reverse order
    printf("\nContents of the file in reverse order:\n");
    for (i = fileSize - 1; i >= 0; i--) {
        printf("%c", fileContents[i]);
    }

    // Free the allocated memory
    free(fileContents);

    return 0;
}
