#include <iostream>
#include <cstdlib>
#include <ctime>
#include <thread>
#include <chrono>

double generateRandomTemperature(double min, double max) {
    double random = (double)rand() / RAND_MAX;
    return min + random * (max - min);
}

double readTemperature() {
    return generateRandomTemperature(20.0, 30.0);
}

void controlSystem(double currentTemperature, double desiredTemperature) {
    if (currentTemperature < desiredTemperature) {
        std::cout << "Heating system: ON" << std::endl;
        std::cout << "Cooling system: OFF" << std::endl;
    } else if (currentTemperature > desiredTemperature) {
        std::cout << "Heating system: OFF" << std::endl;
        std::cout << "Cooling system: ON" << std::endl;
    } else {
        std::cout << "Heating system: OFF" << std::endl;
        std::cout << "Cooling system: OFF" << std::endl;
    }
}

int main() {
    srand(static_cast<unsigned>(time(0)));

    double desiredTemperature = 25.0;

    std::cout << "Enter the desired temperature: ";
    std::cin >> desiredTemperature;

    while (true) {
        double currentTemperature = readTemperature();

        std::cout << "Current Temperature: " << currentTemperature << std::endl;
        std::cout << "Desired Temperature: " << desiredTemperature << std::endl;

        controlSystem(currentTemperature, desiredTemperature);

        std::cout << std::endl;
        std::this_thread::sleep_for(std::chrono::seconds(5));
    }

    return 0;
}
