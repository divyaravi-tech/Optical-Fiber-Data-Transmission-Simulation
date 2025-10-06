# Optical-Fiber-Data-Transmission-Simulation
This project simulates digital data transmission through an optical fiber using light pulse representation
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

void transmit(char *data);
void receive(char *opticalSignal);

int main() {
    char data[100];
    printf("Enter the binary data to send (only 0s and 1s): ");
    scanf("%s", data);

    // Check for invalid input
    for (int i = 0; i < strlen(data); i++) {
        if (data[i] != '0' && data[i] != '1') {
            printf("Error: Only binary digits (0 or 1) allowed.\n");
            return 1;
        }
    }

    printf("\n--- Optical Communication Simulation ---\n");
    transmit(data);

    return 0;
}

void transmit(char *data) {
    char opticalSignal[200] = "";
    printf("\nTransmitting through optical fiber...\n");

    for (int i = 0; i < strlen(data); i++) {
        if (data[i] == '1') {
            strcat(opticalSignal, "LIGHT ");
        } else {
            strcat(opticalSignal, "DARK ");
        }
    }

    printf("Optical Signal Sent: %s\n", opticalSignal);

    // Simulate transmission delay
    printf("Transmitting...\n");
    for (int i = 0; i < 3; i++) {
        printf(".");
        fflush(stdout);
        for (volatile long j = 0; j < 100000000; j++);  // delay
    }

    printf("\nSignal Received Successfully!\n");
    receive(opticalSignal);
}

void receive(char *opticalSignal) {
    char receivedData[100] = "";
    char *token = strtok(opticalSignal, " ");

    while (token != NULL) {
        if (strcmp(token, "LIGHT") == 0) {
            strcat(receivedData, "1");
        } else if (strcmp(token, "DARK") == 0) {
            strcat(receivedData, "0");
        }
        token = strtok(NULL, " ");
    }

    printf("\nDecoded Binary Data at Receiver: %s\n", receivedData);
    printf("Data Transmission Completed Successfully!\n");
}
