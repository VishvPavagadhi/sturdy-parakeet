%Stress in Cantilever beam 
clc
clear all
E = 2e11; % Young's modulus in Pa
I = 1.333e-5; % Moment of inertia in m^4
L = 1; % Length of the beam in m

% Define the loading and unloading forces
F = [1 -1]; % Force in Newtons
num_cycles = 10;

% Initialize the stress vector
stress = zeros(num_cycles*2,1);

% Calculate the maximum stress for each cycle
for i = 1:num_cycles
    % Apply the loading force
    delta = L/1000;
    y = 0:delta:L;
    P = F(mod(i,2)+1);
    w = P/24/E/I*(L^2*y.^2 - 4*L*y.^3 + 3*y.^4);
    stress(2*i-1) = max(abs(w))*I/(2*sqrt(3)*L);

    % % Remove the loading force
    delta = L/1000;
    y = 0:delta:L;
    P = 0;
    w = P/24/E/I*(L^2*y.^2 - 4*L*y.^3 + 3*y.^4);
    stress(2*i) = max(abs(w))*I/(2*sqrt(3)*L);
end

% Plot the stress as a function of time
plot(1:length(stress),stress,'LineWidth',2);
xlabel('Cycle number');
ylabel('Stress (Pa)');
title('Stress vs. cycle number for a cantilever beam');
