function [QRS_n]= Rwave_detection(signal)
    signal_part = signal
    Y2= [];
    for n = 3:(length(signal_part)-2)
        Y0(n) = abs(signal_part(n+1)-signal_part(n-1));
        Y1(n) = abs(signal_part(n+2)-2.*signal_part(n)+signal_part(n-2));
        Y2(end+1) = 8.5*Y0(n) + 8.1*Y1(n);
    end
        QRS_n = [];
        QRS = [] ;
        counter = 0;
        QRS_index = 1;
        for i = 1:length(Y2)-8
           if Y2(i) >= 2000
              for k = 1:8
                 if Y2(i+k) >= 2000
                    counter = counter+1;
                 end
              end
              if counter >= 6
                  QRS(QRS_index) = i;
                  QRS_index = QRS_index+1;
              end
            end
       end

       max_in_seq = 0;
       max_in_seq_i = 0;
       for i =1:(length(QRS))
           value = signal_part(QRS(i));
           if value > max_in_seq
               max_in_seq = value;
                max_in_seq_i = QRS(i);
           end

            if i == length(QRS) || QRS(i+1)-QRS(i)> 275
              QRS_n(end+1) = max_in_seq_i;
              max_in_seq_i = 0;
              max_in_seq = 0;
            end
            for k = 1: length(QRS_n)
              if QRS_n(k) == 0
                QRS_n(k) = [];
              end
            end
        end 
plot(1:length(signal_part),signal_part,QRS_n,signal_part(QRS_n),'o')
title('ECG peaks')
xlabel('Time[S]')
ylabel('Amplitude[mv]')
end
