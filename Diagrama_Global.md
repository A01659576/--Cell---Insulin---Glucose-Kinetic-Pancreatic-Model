```matlab
clear; clc; close all;
```

```matlabTextOutput
Warning: Function ge has the same name as a MATLAB built-in. We suggest you rename the function to avoid a potential name conflict.
Warning: Function ge has the same name as a MATLAB built-in. We suggest you rename the function to avoid a potential name conflict.
```

```matlab
%% Fase 4 - Diagrama Global
% Paulina Leal Mosqueda A01659576, Santiago Nava Figueroa A01174557, Carlo Crivelli Hernández A01656171, %% Ricardo Villareal Bazán A01666859
clear; clc; close all;
%% =====================================================
% PARÁMETROS
% =====================================================
R0 = 864;
Ge = 140;
EGO = 1.44;
SI = 0.72;
sigma = 43.2;
alpha = 20000;
rho = 0.41;
k = 432;
d0 = 0.06;
r1 = 0.84e-3;
r2 = 0.24e-5;

%% =====================================================
% SISTEMA
% =====================================================
f = @(t,y) [
    R0 + Ge - (EGO + SI*y(2))*y(1);
    (y(3)*sigma*y(1)^2)/(alpha + y(1)^2) - (rho + k)*y(2);
    (-d0 + r1*y(1) - r2*y(1)^2)*y(3)
];

%% =====================================================
% EQUILIBRIOS
% =====================================================
E1 = [697.22, 0, 0];
E2 = [100, 11.944, 358.673];
E3 = [250, 3.578, 47.271];

%% =====================================================
% OPCIONES BASE
% =====================================================
options = odeset('RelTol',1e-9,'AbsTol',1e-9);

%% =====================================================
%  Aplicar ODE
% =====================================================
options_E1 = odeset('RelTol',1e-9,'AbsTol',1e-9, ...
    'Events',@(t,y) eventoE1(t,y,E1));

%% =====================================================
% CONDICIONES CERCA DEL PUNTO SILLA E3
% =====================================================
ICs = [
    E3 + [ 1  0  0];
    E3 + [ 0  0.37  0];
];

%% =====================================================
% FIGURA
% =====================================================
figure('Color','w','Position',[100 100 1100 760]);
hold on;
grid on;
box on;
xlabel('G','FontSize',14,'FontWeight','bold');
ylabel('I','FontSize',14,'FontWeight','bold');
zlabel('\beta','FontSize',14,'FontWeight','bold');
title('Plano Fase Global', ...
    'FontSize',15,'FontWeight','bold');
view(45,25);

%% =====================================================
% COLORES
% =====================================================
col1 = [0.85 0.10 0.10];
col2 = [0.05 0.55 0.15];
col3 = [0.10 0.20 0.90];

%% =====================================================
% RANGOS
% =====================================================
xlim([50 750]);
ylim([0 20]);
zlim([0 420]);

%% =====================================================
% TRAYECTORIA DESDE E1 a E0
% =====================================================
IC_E2 = E2 + [0 0 0]; 

% resolver sistema para condiciones iniciales en E2
[tE2,yE2] = ode15s(f,[0 5000],IC_E2,options_E1);
plot3(yE2(:,1),yE2(:,2),yE2(:,3),'k','LineWidth',2.8);

%% =====================================================
% TRAYECTORIAS CERCA DE E2
% =====================================================
% Tomar condiciones iniciales para E2 y resolver sistema
for i = 1:size(ICs,1)
    [t,y] = ode15s(f,[0 5000],ICs(i,:),options_E1);
    plot3(y(:,1),y(:,2),y(:,3),'k','LineWidth',2);
end

%% =====================================================
% Graficar puntos de equilibrio
% =====================================================
scatter3(E1(1),E1(2),E1(3),50,col1,'MarkerFaceColor', [0.15 0.15 0.15], ...
    'MarkerEdgeColor', 'none');
scatter3(E2(1),E2(2),E2(3),50,col2,'MarkerFaceColor', [0.15 0.15 0.15], ...
    'MarkerEdgeColor', 'none');
scatter3(E3(1),E3(2),E3(3),50,col3,'MarkerFaceColor', [0.15 0.15 0.15], ...
    'MarkerEdgeColor', 'none');

text(E1(1)-45, E1(2)+0.3, E1(3)+8,  'E_0','FontSize',13,'FontWeight','bold','Color',col1);
text(E2(1)+10, E2(2)+0.3, E2(3)+8,  'E_1','FontSize',13,'FontWeight','bold','Color',col2);
text(E3(1)+10, E3(2)+0.3, E3(3)+8,  'E_2','FontSize',13,'FontWeight','bold','Color',col3);


% detener simulación una vez que la trayectoria llega a E1
function [val, isterm, dir] = eventoE1(~, y, E1)
    val    = norm(y(:)' - E1) - 5;
    isterm = 1;
    dir    = -1;
end