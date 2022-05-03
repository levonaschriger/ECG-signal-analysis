% transforming from freq to sec
R = (nonzeros(QRS_n))';  
fs = 1500;
R_R = diff(R);
R_in_sec = (1/fs)*R;
R_R_in_sec = (1/fs).*R_R;


%finding T wave
R_R_det_T = {};
T_wave = [];
starting_T = [];
ending_T = [];
for i = 1:(length(R_R)-1)
    starting_T(end+1) = round(R(i) + 0.16*R_R(i+1));
    ending_T(end+1) =  round(R(i) + 0.57*R_R(i+1));
    start_indx = starting_T(i);
    end_indx = ending_T(i);
    R_R_det_T{i} = norm(start_indx:end_indx);
end

%phasor transform
Rv_T = 0.1;
PT_T = {};
phi_T = {};
for i = 1:length(R_R_det_T)
    for n = 1:length(R_R_det_T{i}(:))
        PT_T{i} = Rv_T + j*(R_R_det_T{i}(:));
        phi_T{i} = atand(R_R_det_T{i}(:)./Rv_T);
    end
end

for i = 1:length(R_R_det_T)
    T_wave(end+1) = max(phi_T{i}(:));
end

%finding P wave
det_P = {};
starting_p = [];
ending_p = [];
for i = 1:length(R_R)
    starting_p(i) = round(R(i) - 0.7*R_R(i));
    ending_p(i) =  round(R(i) - 0.07*R_R(i));
    start_indx = starting_p(i);
    end_indx = ending_p(i);
    det_P{i} = norm(start_indx:end_indx);
end

%phasor transform
Rv_P = 0.05;
PT_P = {};
phi_P = {};
for i = 1:length(det_P)
    for n = 1:length(det_P{i}(:))
        PT_P{i} = Rv_P + j*(det_P{i}(:));
        phi_P{i} = atand(det_P{i}(:)./Rv_P);
    end
end

P_pot_1 = [];
for i = 1:length(PT_P)
    P_pot_1(end+1) = max(phi_P{i}(:));
end

P_wave = [];
% is P after T? if so, it is a P wave, if not it's not
for i = 1:length(T_wave)
    if P_pot_1(i) > T_wave(i)
        P_pot_2 = P_pot_1;
   
    %voltage condition
    %voltage_of_P(i) = norm(i);
    %if voltage_of_P > 0.1*(R(i))
        P_wave(end+1) = max(phi_P{i}(:));
    end
end

P_wave_in_sec = (1/fs).*P_wave;
R_R_in_sec = R_R_in_sec(2:end);
%calculating the PR duration
rp_in_sec = [];
pr_in_sec = [];
for i = 1:length(P_wave)
    rp_in_sec(end+1)= R_R_in_sec(i) - P_wave_in_sec(i);
    pr_in_sec(end+1)= R_R_in_sec(i) -rp_in_sec(i);
end

for i = 1:length(pr_in_sec)
    if pr_in_sec(i) > 0.2
        'call nurse  immediately, first degree AV block!!'
    end
end
