%% Task C1vA_CSm 
% This code is © Battaglia et al., 2018, and it is made available
% under the GPL license enclosed with the software.
% 
%
% Over and above the legal restrictions imposed by this license, 
% if you use this software for an academic publication then you are obliged 
% to provide proper attribution. This can be to this code directly.
% 
% 
% Battaglia S., Garofalo S., di Pellegrino G., 
% Context-dependent extinction of threat memories: 
% influences of healthy aging. Scientific Reports, 2018, (8) 12592.

%% INITIALIZATION DRIVERS and PORTS
function initialization_parallel_port()
clc; clear all;

global ioObj;
global address_biopac;
global address_shock;

ioObj = io64;
%load inpout64.dll system driver for parallel port;                        %This .dll should be in the same directory or in C:\Users\xxxx\Documents\MATLAB
status = io64(ioObj);

address_biopac = hex2dec('D050');                                          %trigger for SCR and EMG;
io64(ioObj,address_biopac,0);                                              %set Trigger to zero at the beginning of the script

address_shock = hex2dec('D010');                                           %triggher for shock pulse
io64(ioObj,address_shock,0);                                               %set Trigger to zero at the beginning of the script

fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -\n');
fprintf('\n Let''s start...\n')
check_parallel_port()                                                      %chiama la funzione che esegue un check della funzionalit‡ delle porte parallele

    function check_parallel_port()
        fprintf('\n --> checking parallel port functionalities\n');
        WaitSecs(0.5);
        for check = 1:5
            io64(ioObj,address_biopac,255);                               %open BIOPAC parallel port
            fprintf('trigger BIOPAC ON %d\n',check);
            
            io64(ioObj,address_shock,255);                                %open shock parallel port
            fprintf('trigger shock ON %d\n',check);
                     
            WaitSecs(0.2);
 
            io64(ioObj,address_biopac,0);                                 %close BIOPAC parallel port
            fprintf('trigger BIOPAC OFF %d\n',check);%

            io64(ioObj,address_shock,0);                                  %close schok parallel port
            fprintf('trigger shock OFF %d\n',check);
            
            WaitSecs(0.5);
            fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - \n');
        end
    end

    if check==5
        fprintf('\n --> parallel port is working smoothly, let''s start the task...\n');
        load_specs()
    else
        fprintf('\n - re-check parallel port...\n');
        check_parallel_port()
    end
    
end 

function load_specs()
global input_folder
global output_folder

%MODIFICARE LE FOLDERS SE NECESSARIO (SOLO QUI)
input_folder='C:\SIMONE\Task';
output_folder='C:\SIMONE\Task';

cd(input_folder);

fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -');
fprintf('\n                  Task C1vA                              |\n');
fprintf('%s                                              |\n',date);
fprintf('Context Danger --> Salotto con tavolino                  |\n');
fprintf('Context Safety --> Cucina con tavolo                     |\n');
fprintf('CS+ --> Lampada                                          |\n');
fprintf('CS- --> Pianta                                           |');
fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -\n\n');

opening_function()
end

%% OPENING
function opening_function()
Screen('Preference','SkipSyncTests',1);
rng('shuffle');                                                             %reset dello shuffle;

global nomefile

subj_info();                                                                %funzione per raccogliere le informazioni del partecipante;
     function subj_info()
           prompt={'ID:','Name:','Surname','Group'};                        %testo che verr‡ visualizzato nella finestra;
           name='Extinction Task';                                          %nome finestra;
           numlines=1;                                                      %righe a disposizione per scrivere;
           options.Resize='on';                                             %se si vuole rendere la finestra che compare resizable;
           options.WindowStyle='modal';             
           options.Interpreter='tex';

           infosubj=inputdlg(prompt,name,numlines);                         %permette di visualizzare la finestra di input e salva le informazioni;
           ID=infosubj(1);
           ID=char(ID);
           name=infosubj(2);                                                %prende dall'oggetto il valore relativo al nome;
           name=char(name);                                                 %converte da oggetto a stringa;
           surname=infosubj(3);                                             %prende dall'oggetto il valore relativo al cognome;
           surname=char(surname);                                           %converte da oggetto a stringa;
           group=infosubj(4);                                               %prende dall'oggetto il valore relativo al gruppo;
           group=char(group);
           data_odierna = date;                                             %prende la data attuale dal computer;    
     fprintf('Subject is %s %s %s of %s group \n',ID,name,surname,group);
     end
 
 experimental_session(ID,name,surname, group, data_odierna);                %funzione per scegliere la sessione sperimentale; 
    function experimental_session(ID,name,surname, group, data_odierna)
           ButtonName = questdlg('Which is the experimental session today?', ...
                         'Session', ...
                         'DAY 1', 'DAY 2','xxx');
            switch ButtonName,
                case 'DAY 1',
                  disp('--> Loading Day 1 Experimental Session...');
                  nomefile=strcat(ID,'_',name,'_',surname,'_',group,'_','DAY1_',data_odierna,'_C1vA','.xlsx'); %crea una variabile-stringa che dar‡ il nome al file excel relativa alla prestazione del soggetto; 
                  day_1();
                case 'DAY 2',
                  disp('--> Loading Day 2 Experimental Session...');
                  nomefile=strcat(ID,'_',name,'_',surname,'_',group,'_','DAY2_',data_odierna,'_C1vA','.xlsx'); %crea una variabile-stringa che dar‡ il nome al file excel relativa alla prestazione del soggetto; 
                  day_2();
            end 
    end
end

%% OPENING FUNCTION DAY 1
function day_1()
fprintf('\n--> Creating DAY 1 scenario...\n');
Screen('Preference','SkipSyncTests',1);                                     %comando per skippare dei test di schermo non necessari;

% [finestra, grandezza] = Screen('apreunafinestra',n∞schermo*,[colore_finestra],[0 0 grandexza_x grandezza_y])
    %* se impostiamo 0 --> la finestra di psychtoolbox appare nella stessa schermata in cui c'Ë la barra di start

%[windowPtr, rect] = Screen('OpenWindow',0,[255 255 255],[0 0 1200 600]);   %finestra piccola;
%[windowPtr, rect] = Screen('OpenWindow',0,[125 125 125],[0 0 1280 1024]);  %Monitor Lenovo;
[windowPtr, rect] = Screen('OpenWindow',0,[125 125 125],[0 0 1920 1080]);   %TV

HideCursor;                                                                 %nasconde il mouse durante l'esecuzione del task;

main_day_1(windowPtr,rect);                                                 %chiama la funzione MAIN del 1∞ giorno
end

%%                         / / / MAIN FUNCTION DAY 1 \ \ \
function main_day_1(windowPtr,rect)
global blocchi;             %contatore che tiene traccia dei blocchi;
global counter;             %contatore generico degli item nello script indipendentemente dalla sessione;
global counter_emiblocchi;  %contatore che tiene traccia degli emiblocchi;
global counter_stim;        %contatore che tiene traccia della sequenza degli stimoli che sono stati inviati;
global counter_CS;          %contatore che tiene traccia della sequenza del tipo di CS che Ë stato inviato;
global counter_sess;        %contatore che tiene traccia della sessessione in cui ogni stimolo Ë stato inviato;
global counter_context;     %contatore che tiene traccia del contesto in cui ogni CS Ë stato inviato;
global counter_hab;         %contatore che tiene traccia dei CS inviati nella sessione HABITUATION;
global counter_acq;         %contatore che tiene traccia dei CS inviati nella sessione ACQUISITION;
global counter_ext;         %contatore che tiene traccia dei CS inviati nella sessione EXTINCTION;
global counter_RT_CS;       %contatore che tiene traccia dei Tempi di Reazione
global counter_keyrelease;  %contatore che tiene traccia di quanto tempo il tasto Ë stato premuto;

counter=0;                  %inizializzazione parametro; non viene resettato ogni blocco;
blocchi=1;                  %inizializzazione parametro; non viene resettato ogni blocco;
counter_emiblocchi=1;
counter_hab=1;              %inizializzazione parametro; non viene resettato ogni blocco;
counter_acq=1;              %inizializzazione parametro; MA viene resettato ogni emi-blocco;
counter_ext=1;              %inizializzazione parametro; MA viene resettato ogni emi-blocco;

counter_context={};         %inizializzazione parametro; non viene resettato ogni blocco;
counter_stim={};            %inizializzazione parametro; non viene resettato ogni blocco;
counter_CS={};              %inizializzazione parametro; non viene resettato ogni blocco;
counter_sess={};            %inizializzazione parametro; non viene resettato ogni blocco;                                                   
counter_RT_CS={};           %inizializzazione parametro; non viene resettato ogni blocco;
counter_keyrelease={};      %inizializzazione parametro; non viene resettato ogni blocco;

%Stimuli 60/40
habituation=4;              %numero di trials di Habituation

acquisition=[8 20 12];      %numero di items nella sessione di Acquisition [CS+, CS-, CS+/US (quello che deve essere maggiore dei due CS+)];
extinction=[20 20];         %numero di items nella sessione di Extinction [CS+, CS-];

% acquisition=[2 6 4];       %per fare le prove deve stare in %OFF
% extinction=[2 2];          %per fare le prove deve stare in %OFF

items_day1=(sum(habituation)+sum(acquisition)+sum(extinction));     %numero degli items che verranno inviati nel 1∞ giorno;

disp(' ---> LET''s START ');                                        %mostra in command window che si sta per iniziare il task;
tic;                                                                %cronometro: inizia a tenere il tempo da quando Ë iniziato l'intero task;

fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -\n');
fprintf('\n --> DAY 1 SESSION - includes %d items \n',items_day1);

    for b=1:blocchi   
        ITI(windowPtr,rect)
        %% Habituation 
        fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -\n');
        fprintf('\n --> HABITUATION - includes %d items \n',sum(habituation));
            %Set Stimuli for Habituation
                hab_stimuli={'context_danger_lamp.png','context_danger_pianta.png',...   %definisce gli stimoli in HABITUATION session; 
                             'context_danger_lamp.png','context_danger_pianta.png'};     %devono essere solamente (2CS+ e 2CS- in Acq Context)         
        z=1:habituation;
        while z(1)~=2 %fa in modo che il primo stimolo sia un CS-
            z=z(randperm(length(z)));
        end
        
            for hab=1:habituation                                                        %FOR-loop HABITUATION che regola la presentazione di ogni singolo trial;
                 %fixation(windowPtr,rect);                                              %chiama la funzione che genera il punto di fissazione;
                 task_hab (windowPtr,habituation,hab,hab_stimuli,z)                      %chiama la funzione che gestisce il task per ogni singolo trial in HABITUATION;
                 ITI(windowPtr,rect);                                                    %chiama la funzione che genera ITI;
            end
            
        partial_saving;
        
        %% Acquisition Context Danger
        acquisition=[(acquisition(1)/2) (acquisition(2)/2) (acquisition(3)/2)];
        for x=1:2
            counter_acq=1;                                                                  %reset del parametro per gli emiblocchi;
            fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -\n');
            fprintf('\n --> ACQUISITION - %d∞ Emiblock - includes %d items \n',x,sum(acquisition));
                %Set Stimuli for Acquisition
                  CSp='context_danger_lamp.png';    %CS+ --> Lampada                        %definisce il CS+ in ACQUISITION session;
                  CSm='context_danger_pianta.png';  %CS- --> Pianta                         %definisce il CS- in ACQUISITION session;
                  CSpUS='context_danger_lamp.png';  %CS+/US --> Lampada                     %definisce il CS+/US in ACQUISITION session;
            sequenza_acquisition = seq_acq (acquisition);                                   %chiama la funzione che crea la sequenza degli stimoli in ACQUISITION;
                for acq=1:sum(acquisition)                                                  %FOR-loop ACQUISITION che regola la presentazione di ogni singolo trial;
                    %fixation(windowPtr,rect);                                              %chiama la funzione che genera il punto di fissazione; 
                    task_acq(windowPtr,sequenza_acquisition,acquisition,CSp,CSm,CSpUS,x);   %chiama la funzione che gestisce il task per ogni singolo trial in ACQUISITION;
                    ITI(windowPtr,rect);                                                    %chiama la funzione che genera ITI;        
                end
            partial_saving;                                             %chiama la funzione che permette un salvataggio parziale della prestazione del partecipante;
        end
        
        script_pause(windowPtr,rect);
        
        %% Extinction
        extinction=[(extinction(1)/2) (extinction(2)/2)];
        for y=1:2
            counter_ext=1;   
            fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -\n');
            fprintf('\n --> EXTINCTION - %d∞ Emiblock - includes %d items \n',y,sum(extinction));
                %Set Stimuli for Extinction
                  CSp='context_safety_lamp.png';    %CS+ --> Lampada                %definisce il CS+ in EXTINCTION session;
                  CSm='context_safety_pianta.png';  %CS- --> Pianta                 %definisce il CS- in EXTINCTION session;
            sequenza_extinction = seq_ext (extinction);                             %chiama la funzione che crea la sequenza degli stimoli in EXTINCTION;
                for ext=1:sum(extinction)                                           %FOR-loop EXTINCTION che regola la presentazione di ogni singolo trial;
                    %fixation(windowPtr,rect);                                      %chiama la funzione che genera il punto di fissazione; 
                    task_ext (windowPtr,sequenza_extinction,extinction,CSp,CSm,y);  %chiama la funzione che gestisce il task per ogni singolo trial in EXTINCTION;
                    ITI(windowPtr,rect);                                            %chiama la funzione che genera ITI;        
                end
            partial_saving;                                                 %chiama la funzione che permette un salvataggio parziale della prestazione del partecipante; 
        end
        
        if blocchi > 1                                                      %IF: verifica l'eventuale presenza di blocchi, se si..
            end_block(windowPtr);                                           %chiama la funzione che crea una schemata tra un blocco e l'altro;
        end
        
    end        
    end_task(windowPtr);                                                    %chiama la funzione che salva la performance del soggetto e chiude lo script;
end

%% Function --> Fissazione
function fixation (windowPtr,rect)
%Define cross characteristics
crossLength = 3;
crossColor = 1;
crossWidth = 4;

%Set start and end points of lines
crossLines = [-crossLength, 0; crossLength, 0; 0, -crossLength; 0, crossLength];
crossLines = crossLines';

%Define center of Screen
xCenter = rect(3)/2;
yCenter = rect(4)/2;

%Draw the lines
Screen('DrawLines',windowPtr,crossLines,crossWidth,crossColor,[xCenter,yCenter]);
Screen('Flip',windowPtr);
WaitSecs(2); 
end

%% Function --> TASK di HABITUATION
function task_hab (windowPtr,habituation,hab,hab_stimuli,z)
global ioObj;
global address_biopac;
global counter;
global counter_emiblocchi;
global counter_sess;
global counter_CS;
global counter_stim;
global counter_hab;
global counter_context;
global counter_RT_CS;
global counter_keyrelease;

fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -');
fprintf('\n --> Habituation - il soggetto sta visualizzando item n∞ %d/%d \n',counter_hab,sum(habituation));

counter_sess{counter}='Habituation';
target_file=[];                                                             %inizializzazione e reset parametro
target=z(hab);                                  
target_file=hab_stimuli{target};                                            %seleziona lo stimolo da presentare

    %Salva in una variabile il tipo di Context and CS che Ë stato riprodotto             
    if strcmp(target_file,'context_danger_lamp.png')                        %se quello che sto riprodicendo Ë un CS+ nel contesto danger     
            counter_CS{counter}='CS+';
            disp('This item is Context Danger and CS+');
    
    else if strcmp(target_file,'context_danger_pianta.png')                 %se quello che sto riprodicendo Ë un CS- nel contesto danger
            counter_CS{counter}='CS-';
            disp('This item is Context Danger CS-');
        end
    end
    
    %Image 1/3 - Show Context (DANGER) for 1s before the CS
    context_hab='context_danger.png';
    context=imread(context_hab);                                            %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,context);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    Screen('Flip',windowPtr);                                               %mostra l'immagine;
    disp('Show Context before the CS (for 1s)');
    WaitSecs(1);
    
    %Cronometro del Trial
    time_on = GetSecs();                                                    %cronometro che prende il tempo da quando compare lo stimolo sullo schermo;
    time_off = GetSecs();                                                   %inizializzazione del cronometro di off;
    
    %TRIGGER BIOPAC
    io64(ioObj,address_biopac,255)                                          %apertura trigger BIOPAC che viene dato 0s all'onset e dura 500ms;
    BIOPAC_aperto=1;
    if BIOPAC_aperto==1
        disp('TRIGGER --> BIOPAC Trigger ON');
    else
        disp('****BIOPAC Trigger-ON FAILED!!!');
    end
    
    %Image 2/3 Show CS for Habituation
    stimulus=imread(target_file);                                           %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,stimulus);                     %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    Screen('Flip',windowPtr);                                               %mostra l'immagine;
    disp('Show Stimulus for Habituation (for 4s)');    
    startTime = GetSecs();
    
    %Regola la durata del Trial e TRIGGER BIOPAC
    keyIsDown=0;
    posizione=0;                
    pressed=0; 
    time_pressed=0;
    time_end=0;
    
    while  time_off-time_on<=4                                              %definisce la durata massima del trial e in base al tempo regola i trigger;                                                                                    
        
       time_off= GetSecs();                                                %cronometro: necessario per il while per capire quanto tempo Ë passato dall'onset;
       
       %Trigger BIOPAC 500ms
       if time_off-time_on>=0.5 && BIOPAC_aperto==1;                        %definisce quando il BIOPAC deve essere chiuso (500ms dall'onset);         
       io64(ioObj,address_biopac,0);                                        %Chiusura trigger BIOPAC 500ms dopo essersi aperto;  
          BIOPAC_aperto=0;                                                  
            if BIOPAC_aperto==0
                disp('TRIGGER --> BIOPAC Trigger OFF');
            else
                disp('****BIOPAC Trigger-OFF FAILED!!!');
            end
       end
              
       %Reaction Time to CS and key's Release
       EnableKeys = RestrictKeysForKbCheck([32]);                           %Abilita solamente alcuni tasti da tastiera, in questo caso SPAZIO;
       [keyIsDown, pressedSecs, keyCode] = KbCheck();
       posizione=find(keyCode);
       
       if posizione==32
           time_end=GetSecs();         %key's release
       end
       
       if posizione==32 & pressed==0
            time_pressed=GetSecs();    %RT to CS
            pressed=1;
       end
             
    end %end while
    
    if pressed==1
       counter_RT_CS{counter}=time_pressed-startTime; 
       counter_keyrelease{counter}=(time_end-time_pressed);
       fprintf('\n RT= %.3f seconds\n',counter_RT_CS{counter});
       fprintf('\n Key''s Release= %.3f seconds\n\n',counter_keyrelease{counter});
    else 
       counter_RT_CS{counter}='missed';
       counter_keyrelease{counter}='missed';
       fprintf('\n    NON HA PREMUTO \n\n');
    end
    
    %Image 3/3 - Show Context (DANGER) for 1s after the CS
    context_hab='context_danger.png';
    context=imread(context_hab);                                            %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,context);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    Screen('Flip',windowPtr);                                               %mostra l'immagine;
    disp('Show Context after the CS (for 1s)'); 
    WaitSecs(1);
    
    counter_emiblocchi(counter)=1;
    counter_hab=(counter_hab+1);                                            %aggiornamento counter Habituation (tiene conto di quanti stim son stati presentati);
    counter_stim{counter}=target_file;                                      %aggiornamento counter stimoli (scrive che stimolo Ë stato presentato in questo trial);
    counter_context{counter}='vedere CS_List';                              %aggiornamento counter contesto (scrive che contesto Ë stato presentato in questo trial);
end

%% Function --> Sequenza ACQUISITION
function sequenza_acquisition = seq_acq (acquisition)
item_CSp=ones(1,acquisition(1));                                            %se Ë un 1 sar‡ un CS+
item_CSm=zeros(1,acquisition(2));                                           %se Ë uno 0 sar‡ CS-
item_CSpUS=ones(1,acquisition(3))*2;                                        %se Ë uno 2 sar‡ CS+US
sequenza_acquisition=[item_CSp,item_CSm,item_CSpUS];
sequenza_acquisition=Shuffle(sequenza_acquisition);

sequenza_sbagliata=1;
errore_sequenza=0;

while sequenza_sbagliata==1 %fa in modo che i primi due non siano uguali
    if (sequenza_acquisition(1)==sequenza_acquisition(2))...
       || (sequenza_acquisition(1)==2)...
       || (sequenza_acquisition(2)==2)
            errore_sequenza=1;
    else    %fa in modo che non vi siano pi˘ di due ripetizioni uguali di fila
        for z=1:length(sequenza_acquisition)-3
            if (sequenza_acquisition(z)==sequenza_acquisition(z+1)...
                 && sequenza_acquisition(z)==sequenza_acquisition(z+2)) %...
%                  && sequenza_acquisition(z)==sequenza_acquisition(z+3))
                errore_sequenza=1;
            end
        end
        if sequenza_acquisition(1)~=0 %fa in modo che il primo sia un CS-(0)
            sequenza_acquisition=Shuffle(sequenza_acquisition);
            errore_sequenza=1;
        end
    end
    
    if errore_sequenza==1 %se trova errori ri-mescola
        sequenza_acquisition=Shuffle(sequenza_acquisition);
        errore_sequenza=0;
    else  %se non ci sono errori esci dal while
        sequenza_sbagliata=0;
    end
end
end

%% Function --> TASK di ACQUISITION
function task_acq(windowPtr,sequenza_acquisition,acquisition,CSp,CSm,CSpUS,x)
global ioObj;
global address_biopac;
global address_shock;
global counter;
global counter_emiblocchi;
global counter_CS;
global counter_stim;
global counter_sess;
global counter_acq;
global counter_context;
global counter_RT_CS;
global counter_keyrelease; 

fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -');
fprintf('\n --> Acquisition - il soggetto sta visualizzando item n∞%d/%d del %d∞ EmiBlocco \n',counter_acq,sum(acquisition),x)

counter_sess{counter}='Acquisition';
target_file=[];                                                             %inizializzazione e reset parametro;

    if sequenza_acquisition(counter_acq) == 1                               %se il valore della sequenza Ë 1;
        target_file=CSp;                                                    %allora Ë un CS+;
    else if sequenza_acquisition(counter_acq) == 0                          %se il valore della sequenza Ë 0;
        target_file=CSm;                                                    %allora Ë un CS-;
    else if sequenza_acquisition(counter_acq) == 2                          %se il valore della sequenza Ë 2;
        target_file=CSpUS;                                                  %allora Ë un CS+/US;
    else
        disp('!!!errore nella selezione del CS!!!');                            
        end
        end
    end

    %Salva in una variabile il tipo di CS che Ë stato riprodotto
     if strcmp(target_file,CSp)                                             %se il target file Ë un CS+
        devodarelascossa = sequenza_acquisition(counter_acq);               %valore che indica se deve dare o meno la scossa, essendo un CS+
        if devodarelascossa==2                                              %target file Ë un CS+/US
            devodarelascossa = 1;                                           %scossa verr‡ accesa, essendo un CS+/US
            counter_CS{counter}='CS+/US';
            disp('This item is CS+/US');
            disp('SHOCK MUST be released!');
        else
            devodarelascossa = 0;                                           %target file Ë un CS+ senza scossa
            counter_CS{counter}='CS+';
            disp('This item is CS+');
            disp('NO shock will be released');
        end
     else                                                                   %se non sto riproducendo il CS+, allora sto riproducendo il CS-
        devodarelascossa = 0;                                               %scossa spenta, essendo un CS-
        counter_CS{counter}='CS-';
        disp('This item is CS-');
        disp('NO shock will be released');
     end

    %Image 1/3 - Show Context (DANGER) for 1s before the CS
    context_acq='context_danger.png';
    context=imread(context_acq);                                            %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,context);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    Screen('Flip',windowPtr);                                               %mostra l'immagine;
    disp('Show Context before the CS (for 1s)');
    WaitSecs(1);

    %Cronometro del Trial
    time_on = GetSecs();                                                    %cronometro che prende il tempo da quando compare lo stimolo sullo schermo;
    time_off = GetSecs();                                                   %inizializzazione del cronometro di off;
    
    %TRIGGER BIOPAC
    io64(ioObj,address_biopac,255)                                %apertura trigger BIOPAC che viene dato a 0s all'onset e dura 500ms;
    BIOPAC_aperto=1;
    if BIOPAC_aperto==1
        disp('TRIGGER --> BIOPAC Trigger ON');
    else
        disp('****BIOPAC Trigger-ON FAILED!!!');
    end
    
    %Image 2/3 - Show Context (DANGER) and...
    context_acq='context_danger.png';
    context=imread(context_acq);                                            %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,context);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    
    %Image 3/4 - ... show CS 
    cs=(target_file);
    picture=imread(cs);                                                     %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,picture);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    disp('Show Context and CS (for 4s)');
    Screen('Flip',windowPtr);                                               %mostra l'immagine;
    startTime = GetSecs();                                                  %se devo prende i tempi di reazione di un'immagine mettere il flip dell'immagine prima di GetSecs
        
    %Regola la durata del Trial e i TRIGGER
    scossa_aperta=0;                                                        %parametro di sicurezza per tenere la scossa spenta;
    keyIsDown=0;
    posizione=0;                
    pressed=0; 
    time_pressed=0;
    time_end=0;
    
    while  time_off - time_on <= 4                                          %definisce la durata massima del trial e in base al tempo regola i trigger;

        time_off=GetSecs();                                                 %cronometro: necessario per il while per capire quanto tempo Ë passato dall'onset; 
        
        if time_off - time_on >= 0.5 && BIOPAC_aperto==1;                   %definisce quando il BIOPAC deve essere chiuso (500ms dall'onset);       
              io64(ioObj,address_biopac,0);                         %chiusura trigger BIOPAC 500ms dopo essersi aperto;
              BIOPAC_aperto=0;                                              
                if BIOPAC_aperto==0
                  disp('TRIGGER --> BIOPAC Trigger OFF');
                else
                  disp('****BIOPAC Trigger-OFF FAILED!!!');
                end
         end
       
         if time_off - time_on >= 3.80 && devodarelascossa==1 && scossa_aperta==0
           io64(ioObj,address_shock, 255);                          %apertura trigger per la scossa a 2800 ms dall'onset e dura 200ms;
              scossa_aperta=1;
                if scossa_aperta==1
                    disp('TRIGGER --> Shock Trigger ON');
                else
                    disp('****Shock Trigger-ON FAILED!!!');
                end
         end
         
       %Reaction Time to CS and key's Release
       EnableKeys = RestrictKeysForKbCheck([32]);                           %Abilita solamente alcuni tasti da tastiera, in questo caso SPAZIO;
       [keyIsDown, pressedSecs, keyCode] = KbCheck();
       posizione=find(keyCode);
       
       if posizione==32
           time_end=GetSecs();         %key's release
       end
       
       if posizione==32 & pressed==0
            time_pressed=GetSecs();    %RT to CS
            pressed=1;
       end
         
    end %end while
    
    if pressed==1
       counter_RT_CS{counter}=time_pressed-startTime; 
       counter_keyrelease{counter}=(time_end-time_pressed);
       fprintf('\n RT= %.3f seconds\n',counter_RT_CS{counter});
       fprintf('\n Key''s Release= %.3f seconds\n\n',counter_keyrelease{counter});
    else 
       counter_RT_CS{counter}='missed';
       counter_keyrelease{counter}='missed';
       fprintf('\n    NON HA PREMUTO \n\n');
    end
    
    io64(ioObj,address_shock, 0);                                           %chiusura trigger per la scossa a 3000 ms e coincide con la fine del CS
    
    scossa_aperta=0;
    if scossa_aperta==0
        disp('TRIGGER --> Shock Trigger OFF');
    else
        disp('****Shock Trigger-OFF FAILED!!!');
    end
    
    %Image 4/4 - Show Context (DANGER) for 1s after the CS
    context_acq='context_danger.png';
    context=imread(context_acq);                                            %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,context);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    Screen('Flip',windowPtr);                                               %mostra l'immagine;
    disp('Show Context after the CS (for 1s)'); 
    WaitSecs(1);
    
    if x == 1
        counter_emiblocchi(sum(counter,counter_acq))=1;
    else 
        counter_emiblocchi(sum(counter,counter_acq))=2;
    end
    
    counter_acq=(counter_acq+1);                                            %aggiornamento counter Acquisition (tiene conto di quanti stim son stati presentati);
    counter_stim{counter}=target_file;                                      %aggiornamento counter stimoli (scrive che stimolo Ë stato presentato in questo trial);
    counter_context{counter}=context_acq;                                   %aggiornamento counter contesto (scrive che contesto Ë stato presentato in questo trial);
end

%% Function --> Sequenza EXTINCTION
function sequenza_extinction = seq_ext (extinction)
item_CSp=ones(1,extinction(1));                                             %se Ë un 1 sar‡ un CS+
item_CSm=zeros(1,extinction(2));                                            %se Ë uno 0 sar‡ CS-
sequenza_extinction=[item_CSp,item_CSm];
sequenza_extinction=Shuffle(sequenza_extinction);

sequenza_sbagliata=1;
errore_sequenza=0;

while sequenza_sbagliata==1 %fa in modo che i primi due non siano uguali
    if sequenza_extinction(1)==sequenza_extinction(2)
        errore_sequenza=1;
    else    %fa in modo che non vi siano pi˘ di due ripetizioni uguali di fila
        for z=1:length(sequenza_extinction)-3
            if (sequenza_extinction(z)==sequenza_extinction(z+1)...
                 && sequenza_extinction(z)==sequenza_extinction(z+2)) %...
%                  && sequenza_extinction(z)==sequenza_extinction(z+3))
                errore_sequenza=1;
            end
        end
    end
    
    if errore_sequenza==1   %se trova errori ri-mescola
        sequenza_extinction=Shuffle(sequenza_extinction);
        errore_sequenza=0;
    else        %se non ci sono errori esci dal while
        sequenza_sbagliata=0; 
    end
end

end

%% Function --> TASK EXTINCTION
function task_ext (windowPtr,sequenza_extinction,extinction,CSp,CSm,y)
global ioObj;
global address_biopac;
global counter;
global counter_emiblocchi;
global counter_sess;
global counter_CS;
global counter_stim;
global counter_ext;
global counter_context;
global counter_RT_CS;
global counter_keyrelease; 

fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -');
fprintf('\n --> Extinction - il soggetto sta visualizzando item n∞%d/%d del %d∞ EmiBlocco \n',counter_ext,sum(extinction),y);

counter_sess{counter}='Extinction';
target_file=[];                                                             %inizializzazione e reset parametro

    if sequenza_extinction(counter_ext) == 1                                %se il valore della sequenza Ë 1;
        target_file=CSp;                                                    %allora Ë un CS+;
    else if sequenza_extinction(counter_ext) == 0                           %se il valore della sequenza Ë 0;
        target_file=CSm;                                                    %allora Ë un CS-;
    else 
        disp('!!!errore nella selezione del CS!!!');  
        end
    end 

%Salva in una variabile il tipo di CS che Ë stato riprodotto             
    if strcmp(target_file,CSp)                                              %se il target file Ë un CS+;     
        counter_CS{counter}='CS+';
        disp('This item is CS+');
    else                                                                    %se non sto riproducendo il CS+, allora sto riproducendo il CS-;
        counter_CS{counter}='CS-';
        disp('This item is CS-');
    end

    %Image 1/4 - Show Context (SAFETY) before the CS for 1s
    context_ext='context_safety.png';
    context=imread(context_ext);                                            %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,context);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    Screen('Flip',windowPtr);                                               %mostra l'immagine;
    disp('Show Context before the CS (for 1s)');
    WaitSecs(1);    

    %Cronometro del Trial
    time_on = GetSecs();                                                    %cronometro che prende il tempo da quando compare lo stimolo sullo schermo;
    time_off = GetSecs();                                                   %inizializzazione del cronometro di off;
    
    %TRIGGER BIOPAC
    io64(ioObj,address_biopac,255)                                          %apertura trigger BIOPAC che viene dato a 0s all'onset e dura 500ms;
    BIOPAC_aperto=1;
    if BIOPAC_aperto==1
        disp('TRIGGER --> BIOPAC Trigger ON');
    else
        disp('****BIOPAC Trigger-ON FAILED!!!');
    end
    
    %Image 2/4 - Show Context (SAFETY) and ...
    context='context_safety.png';
    picture=imread(context);                                                %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,picture);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              

    %Image 3/4 - ... Show CS for 4s
    cs=(target_file);
    picture=imread(cs);                                                     %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,picture);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    disp('Show Context and CS (for 4s)');                 
    Screen('Flip',windowPtr);                                               %mostra l'immagine;
    startTime = GetSecs();
    
    %Regola la durata del Trial e TRIGGER BIOPAC
    keyIsDown=0;
    posizione=0;                
    pressed=0;
    time_pressed=0;
    time_end=0;
    
    while  time_off-time_on<=4                                              %definisce la durata massima del trial e in base al tempo regola i trigger;
    
        time_off=GetSecs();                                                 %cronometro: necessario per il while per capire quanto tempo Ë passato dall'onset;
       
        if time_off-time_on>=0.5 && BIOPAC_aperto==1;                       %definisce quando il BIOPAC deve essere chiuso (500ms dall'onset);
        io64(ioObj,address_biopac,0);
          BIOPAC_aperto=0;                                                  %chiusura trigger BIOPAC 500ms dopo essersi aperto;
            if BIOPAC_aperto==0
                disp('TRIGGER --> BIOPAC Trigger OFF');
            else
                disp('****BIOPAC Trigger-OFF FAILED!!!');
            end
        end
       
       %Reaction Time to CS and key's Release
       EnableKeys = RestrictKeysForKbCheck([32]);                           %Abilita solamente alcuni tasti da tastiera, in questo caso SPAZIO;
       [keyIsDown, pressedSecs, keyCode] = KbCheck();
       posizione=find(keyCode);
       
       if posizione==32
           time_end=GetSecs();         %key's release
       end
       
       if posizione==32 & pressed==0
            time_pressed=GetSecs();    %RT to CS
            pressed=1;
       end
         
    end %end while
    
    if pressed==1
       counter_RT_CS{counter}=time_pressed-startTime; 
       counter_keyrelease{counter}=(time_end-time_pressed);
       fprintf('\n RT= %.3f seconds\n',counter_RT_CS{counter});
       fprintf('\n Key''s Release= %.3f seconds\n\n',counter_keyrelease{counter});
    else 
       counter_RT_CS{counter}='missed';
       counter_keyrelease{counter}='missed';
       fprintf('\n    NON HA PREMUTO \n\n');
    end
    
    %Image 4/4 - Show Context (SAFETY) for 1s after the CS
    context_ext='context_safety.png';
    context=imread(context_ext);                                            %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,context);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    Screen('Flip',windowPtr);                                               %mostra l'immagine;
    disp('Show Context after the CS (for 1s)');
    WaitSecs(1);
    
    if y == 1
        counter_emiblocchi(sum(counter,counter_ext))=1;
    else 
        counter_emiblocchi(sum(counter,counter_ext))=2;
    end
    
    counter_ext=(counter_ext+1);                                            %aggiornamento counter Extinction (tiene conto di quanti stim son stati presentati);
    counter_stim{counter}=target_file;                                      %aggiornamento counter stimoli (scrive che stimolo Ë stato presentato in questo trial);
    counter_context{counter}=context_ext;                                   %aggiornamento counter contesto (scrive che contesto Ë stato presentato in questo trial);
                                
end

%% OPENING FUNCTION DAY 2 SESSION
function day_2()
fprintf('\n--> Creating DAY 2 scenario...\n');
Screen('Preference','SkipSyncTests',1);                                     %comando per skippare dei test di schermo non necessari;

% [finestra, grandezza] = Screen('apreunafinestra',n∞schermo*,[colore_finestra],[0 0 grandexza_x grandezza_y])
    %* se impostiamo 0 --> la finestra di psychtoolbox appare nella stessa schermata in cui c'Ë la barra di start

%[windowPtr, rect] = Screen('OpenWindow',0,[255 255 255],[0 0 1200 600]);   %finestra piccola;
%[windowPtr, rect] = Screen('OpenWindow',0,[255 255 255],[0 0 1600 1300]);  %full-screen monitor Samsung;
%[windowPtr, rect] = Screen('OpenWindow',0,[125 125 125],[0 0 1280 1024]);  %Monitor Lenovo
[windowPtr, rect] = Screen('OpenWindow',0,[125 125 125],[0 0 1920 1080]);   %TV

HideCursor;                                                                %nasconde il mouse durante l'esecuzione del task;

main_day_2(windowPtr,rect);                                                 %chiama la funzione MAIN del 2∞ giorno;
end

%%                         / / / MAIN FUNCTION DAY 2 \ \ \
function main_day_2(windowPtr,rect)
global blocchi;             %contatore che tiene traccia dei blocchi;
global counter;             %contatore generico degli item nello script indipendentemente dalla sessione;
global counter_emiblocchi;  %contatore che tiene traccia dei blocchi;
global counter_stim;        %contatore che tiene traccia della sequenza degli stimoli che sono stati inviati;
global counter_CS;          %contatore che tiene traccia della sequenza del tipo di CS che Ë stato inviato;
global counter_sess;        %contatore che tiene traccia della sessessione in cui ogni stimolo Ë stato inviato;
global counter_context;     %contatore che tiene traccia del contesto in cui ogni CS Ë stato inviato;
global counter_ext_rec;     %contatore che tiene traccia dei CS inviati nella sessione EXTINCTION RECALL;
global counter_renewal;     %contatore che tiene traccia dei CS inviati nella sessione RENEWAL;
global counter_RT_CS;       %contatore che tiene traccia dei RT inviati nella sessione RENEWAL;
global counter_keyrelease; 

counter=0;                  %inizializzazione parametro; non viene resettato ogni blocco;
blocchi=1;                  %inizializzazione parametro; non viene resettato ogni blocco;
counter_emiblocchi=1;       %inizializzazione parametro; non viene resettato ogni blocco;
counter_ext_rec=1;          %inizializzazione parametro; MA viene resettato ogni emiblocco;
counter_renewal=1;          %inizializzazione parametro; MA viene resettato ogni emiblocco;

counter_context={};         %inizializzazione parametro; non viene resettato ogni blocco;
counter_stim={};            %inizializzazione parametro; non viene resettato ogni blocco;
counter_CS={};              %inizializzazione parametro; non viene resettato ogni blocco;
counter_sess={};            %inizializzazione parametro; non viene resettato ogni blocco;                                                                                  
counter_RT_CS={};           %inizializzazione parametro; non viene resettato ogni blocco;
counter_keyrelease={};      %inizializzazione parametro; non viene resettato ogni blocco;

%Stimuli
extinction_recall=[10 10];  %numero di items nella sessione di extinction recall [CS+, CS-];
renewal=[10 10];            %numero di items nella sessione di renewal [CS+, CS-];

%extinction_recall=[2 2];    %per fare le prove deve stare in %OFF     
%renewal=[2 2];              %per fare le prove deve stare in %OFF

items_day2=(sum(extinction_recall)+sum(renewal));                           %numero degli items che verranno inviati nel 2∞ giorno;

tic;                                                                        %cronometro: inizia a tenere il tempo da quando Ë iniziato l'intero task;

fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -\n');
fprintf('\n --> DAY 2 SESSION - includes %d items \n',items_day2);

    for b=1:blocchi   
        ITI(windowPtr,rect)
        %% Extinction Recall
        extinction_recall=[extinction_recall(1)/2 extinction_recall(2)/2];
        for z=1:2
            counter_ext_rec=1;                                                                          %reset del parametro per gli emiblocchi;
            fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -\n');
            fprintf('\n --> EXTINCTION RECALL - %d∞ Emiblock - includes %d items \n',z,sum(extinction_recall));
                %Set Stimuli for Extinction Recall
                  CSp='context_safety_lamp.png';    %CS+ --> Lampada                                    %definisce il CS+ in EXTINCTION RECALL session;
                  CSm='context_safety_pianta.png';  %CS- --> Pianta                                     %definisce il CS- in EXTINCTION RECALL session;
            sequenza_extinction_recall = seq_ext_recall (extinction_recall);                            %chiama la funzione che crea la sequenza degli stimoli in EXTINCTION RECALL;
                for ext=1:sum(extinction_recall)                                                        %FOR-loop EXTINCTION RECALL che regola la sequenza di ogni singolo trial;
                    %fixation(windowPtr,rect);                                                          %chiama la funzione che genera il punto di fissazione; 
                    task_ext_recall(windowPtr,sequenza_extinction_recall,extinction_recall,CSp,CSm,z);  %chiama la funzione che gestisce il task per ogni singolo trial in EXTINCTION RECALL;
                    ITI(windowPtr,rect);                                                                %chiama la funzione che genera ITI;        
                end
            partial_saving;                                                 %chiama la funzione che permette un salvataggio parziale della prestazione del partecipante;       
        end
        
        script_pause(windowPtr,rect);
        
        %% Renewal
        renewal=[renewal(1)/2 renewal(2)/2];
        for j=1:2
            counter_renewal=1;                                                                          %reset del parametro per gli emiblocchi;
            fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -\n');
            fprintf('\n --> RENEWAL - %d∞ Emiblock - includes %d items \n',j,sum(renewal));
                %Set Stimuli for Renewal
                  CSp='context_danger_lamp.png';    %CS+ --> Lampada                                    %definisce il CS+ in EXTINCTION RECALL session;
                  CSm='context_danger_pianta.png';  %CS- --> Pianta                                     %definisce il CS- in EXTINCTION RECALL session;
            sequenza_renewal = seq_renewal (renewal);                                                   %chiama la funzione che crea la sequenza degli stimoli in RENEWAL;
                for ren=1:sum(renewal)                                                                  %FOR-loop RENEWAL che regola la sequenza di ogni singolo trial;
                    %fixation(windowPtr,rect);                                                          %chiama la funzione che genera il punto di fissazione; 
                    task_renewal(windowPtr,sequenza_renewal,renewal,CSp,CSm,j);                         %chiama la funzione che gestisce il task per ogni singolo trial in RENEWAL;
                    ITI(windowPtr,rect);                                                                %chiama la funzione che genera ITI;        
                end
            partial_saving;                                                 %chiama la funzione che permette un salvataggio parziale della prestazione del partecipante; 
        end
        
        if blocchi > 1
            end_block(windowPtr);                                           %chiama la funzione che crea una schemata tra un blocco e l'altro; 
        end
        
    end        
end_task(windowPtr);                                                        %chiama la funzione che salva la performance del soggetto e chiude lo script;
end

%% Function --> Sequenza EXTINCTION RECALL
function sequenza_extinction_recall = seq_ext_recall (extinction_recall)

item_CSp=ones(1,extinction_recall(1));                                      %se Ë un 1 sar‡ un CS+
item_CSm=zeros(1,extinction_recall(2));                                     %se Ë uno 0 sar‡ CS-
sequenza_extinction_recall=[item_CSp,item_CSm];
sequenza_extinction_recall=Shuffle(sequenza_extinction_recall);

sequenza_sbagliata=1;
errore_sequenza=0;

while sequenza_sbagliata==1 %fa in modo che i primi due non siano uguali
    if sequenza_extinction_recall(1)==sequenza_extinction_recall(2)
        errore_sequenza=1;
    else    %fa in modo che non vi siano pi˘ di due ripetizioni uguali di fila
        for z=1:length(sequenza_extinction_recall)-3
            if (sequenza_extinction_recall(z)==sequenza_extinction_recall(z+1)...
                 && sequenza_extinction_recall(z)==sequenza_extinction_recall(z+2)) %...
%                  && sequenza_extinction(z)==sequenza_extinction(z+3))
                errore_sequenza=1;
            end
        end
    end
    
    if errore_sequenza==1   %se trova errori ri-mescola
        sequenza_extinction_recall=Shuffle(sequenza_extinction_recall);
        errore_sequenza=0;
    else        %se non ci sono errori esci dal while
        sequenza_sbagliata=0; 
    end
end

end

%% Function --> TASK EXTINCTION RECALL
function task_ext_recall(windowPtr,sequenza_extinction_recall,extinction_recall,CSp,CSm,z)
global ioObj;
global address_biopac;
global counter;
global counter_emiblocchi;
global counter_sess;
global counter_CS;
global counter_stim;
global counter_ext_rec;
global counter_context;
global counter_RT_CS;
global counter_keyrelease; 

fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -');
fprintf('\n --> Extinction Recall - il soggetto sta visualizzando item n∞%d/%d del %d Emiblocco \n',counter_ext_rec,sum(extinction_recall),z);

counter_sess{counter}='Extinction Recall';
target_file=[];                                                             %inizializzazione e reset parametro

    if sequenza_extinction_recall(counter_ext_rec) == 1                     %se il valore della sequenza Ë 1;
        target_file=CSp;                                                    %allora Ë un CS+;
    else if sequenza_extinction_recall(counter_ext_rec) == 0                %se il valore della sequenza Ë 0;
        target_file=CSm;                                                    %allora Ë un CS-;
        else 
            disp('!!!errore nella selezione del CS!!!');
        end
    end 

    %Salva in una variabile il tipo di CS che Ë stato riprodotto
    if strcmp(target_file,CSp)                                              %se il target file Ë un CS+;
            counter_CS{counter}='CS+';
            disp('The item is CS+');
    else if strcmp(target_file,CSm)                                         %se non sto riproducendo il CS+, allora sto riproducendo il CS-;
            counter_CS{counter}='CS-';
            disp('The item is CS-');
        end
    end

    %Image 1/4 - Show Context (SAFETY) before the CS for 1s
    context_ext_rec='context_safety.png';
    context=imread(context_ext_rec);                                        %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,context);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    Screen('Flip',windowPtr);                                               %mostra l'immagine;
    disp('Show Context before the CS (for 1s)');
    WaitSecs(1);       

    %Cronometro del Trial
    time_on = GetSecs();                                                    %cronometro che prende il tempo da quando compare lo stimolo sullo schermo;
    time_off = GetSecs();                                                   %inizializzazione del cronometro di off;
    
    %TRIGGER BIOPAC
    io64(ioObj,address_biopac,255)                                %apertura trigger BIOPAC che viene dato a 0ms all'onset e dura 500ms;
    BIOPAC_aperto=1;
    if BIOPAC_aperto==1
        disp('TRIGGER --> BIOPAC Trigger ON');
    else
        disp('****BIOPAC Trigger-ON FAILED!!!');
    end
    
    %Image 2/4 - Show Context (SAFETY) and...
    context='context_safety.png';
    picture=imread(context);                                                %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,picture);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
          
    %Image 3/4 - ...Show CS for 4s
    cs=(target_file);
    picture=imread(cs);                                                     %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,picture);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    disp('Show Context and CS (for 4s)');               
    Screen('Flip',windowPtr);                                               %mostra l'immagine;
    startTime = GetSecs();

    %Regola la durata del Trial e TRIGGER BIOPAC
    keyIsDown=0;
    posizione=0;                
    pressed=0; 
    time_pressed=0;
    time_end=0;
    
    while  time_off-time_on<=4                                              %definisce la durata massima del trial e in base al tempo regola i trigger;
        
        time_off=GetSecs();                                                 %cronometro: necessario per il while per capire quanto tempo Ë passato dall'onset;
       
       if time_off-time_on>=0.5 && BIOPAC_aperto==1;                        %definisce quando il BIOPAC deve essere chiuso (500ms dall'onset);
          io64(ioObj,address_biopac,0);                           %chiusura trigger BIOPAC 500ms dopo essersi aperto;
          BIOPAC_aperto=0;
          if BIOPAC_aperto==0
                disp('TRIGGER --> BIOPAC Trigger OFF');
          else
                disp('****BIOPAC Trigger-OFF FAILED!!!');
          end
       end
       
       %Reaction Time to CS and key's Release
       EnableKeys = RestrictKeysForKbCheck([32]);                           %Abilita solamente alcuni tasti da tastiera, in questo caso SPAZIO;
       [keyIsDown, pressedSecs, keyCode] = KbCheck();
       posizione=find(keyCode);
       
       if posizione==32
           time_end=GetSecs();         %key's release
       end
       
       if posizione==32 & pressed==0
            time_pressed=GetSecs();    %RT to CS
            pressed=1;
       end
             
    end %end while
    
    if pressed==1
       counter_RT_CS{counter}=time_pressed-startTime; 
       counter_keyrelease{counter}=(time_end-time_pressed);
       fprintf('\n RT= %.3f seconds\n',counter_RT_CS{counter});
       fprintf('\n Key''s Release= %.3f seconds\n\n',counter_keyrelease{counter});
    else 
       counter_RT_CS{counter}='missed';
       counter_keyrelease{counter}='missed';
       fprintf('\n    NON HA PREMUTO \n\n');
    end

    %Image 4/4 - Show Context (SAFETY) for 1s after the CS
    context_ext_rec='context_safety.png';
    context=imread(context_ext_rec);                                        %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,context);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    Screen('Flip',windowPtr);                                               %mostra l'immagine;
    disp('Show Context after the CS (for 1s)');
    WaitSecs(1);
    
    if z == 1
        counter_emiblocchi(sum(counter,counter_ext_rec))=1;
    else
        counter_emiblocchi(sum(counter,counter_ext_rec))=2;
    end
    
    counter_ext_rec=(counter_ext_rec+1);                                    %aggiornamento counter Extinction Recall (tiene conto di quanti stim son stati presentati);
    counter_stim{counter}=target_file;                                      %aggiornamento counter stimoli (scrive che stimolo Ë stato presentato in questo trial);
    counter_context{counter}=context_ext_rec;                               %aggiornamento counter contesto (scrive che contesto Ë stato presentato in questo trial);
end

%% Function --> Sequenza RENEWAL
function sequenza_renewal = seq_renewal (renewal)

item_CSp=ones(1,renewal(1));                                                %se Ë un 1 sar‡ un CS+
item_CSm=zeros(1,renewal(2));                                               %se Ë uno 0 sar‡ CS-
sequenza_renewal=[item_CSp,item_CSm];
sequenza_renewal=Shuffle(sequenza_renewal);

sequenza_sbagliata=1;
errore_sequenza=0;

while sequenza_sbagliata==1 %fa in modo che i primi due non siano uguali
    if sequenza_renewal(1)==sequenza_renewal(2)
        errore_sequenza=1;
    else    %fa in modo che non vi siano pi˘ di due ripetizioni uguali di fila
        for z=1:length(sequenza_renewal)-3
            if (sequenza_renewal(z)==sequenza_renewal(z+1)...
                 && sequenza_renewal(z)==sequenza_renewal(z+2)) %...
%                  && sequenza_extinction(z)==sequenza_extinction(z+3))
                errore_sequenza=1;
            end
        end
    end
    
    if errore_sequenza==1   %se trova errori ri-mescola
        sequenza_renewal=Shuffle(sequenza_renewal);
        errore_sequenza=0;
    else        %se non ci sono errori esci dal while
        sequenza_sbagliata=0; 
    end
end

end

%% Function --> TASK RENEWAL
function task_renewal(windowPtr,sequenza_renewal,renewal,CSp,CSm,j)
global ioObj;
global address_biopac;
global counter;
global counter_emiblocchi;
global counter_sess;
global counter_CS;
global counter_stim;
global counter_renewal;
global counter_context;
global counter_RT_CS;
global counter_keyrelease; 

fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -');
fprintf('\n --> Renewal - il soggetto sta visualizzando item n∞%d/%d del %d Emiblocco \n',counter_renewal,sum(renewal),j);

counter_sess{counter}='Renewal';
target_file=[];                                                             %inizializzazione e reset parametro;

    if sequenza_renewal(counter_renewal) == 1                               %se il valore della sequenza Ë 1;
            target_file=CSp;                                                %allora Ë un CS+;
    else if sequenza_renewal(counter_renewal) == 0                          %se il valore della sequenza Ë 0;
            target_file=CSm;                                                %allora Ë un CS-;
        else 
            disp('!!!errore nella selezione del CS!!!');
        end
    end 

    %Salva in una variabile il tipo di CS che Ë stato riprodotto
    if strcmp(target_file,CSp)                                              %se il target file Ë un CS+;
            counter_CS{counter}='CS+';
            disp('The item is CS+');
    else if strcmp(target_file,CSm)                                         %se non sto riproducendo il CS+, allora sto riproducendo il CS-;
            counter_CS{counter}='CS-';
            disp('The item is CS-');
        end
    end

    %Image 1/4 - Show Context (DANGER) before the CS
    context_ren='context_danger.png';
    context=imread(context_ren);                                            %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,context);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    Screen('Flip',windowPtr);                                               %mostra l'immagine;
    disp('Show Context before the CS (for 1s)');
    WaitSecs(1);   
    
    %Cronometro del Trial
    time_on = GetSecs();                                                    %cronometro che prende il tempo da quando compare lo stimolo sullo schermo;
    time_off = GetSecs();                                                   %inizializzazione del cronometro di off;
    
    %TRIGGER BIOPAC
    io64(ioObj,address_biopac,255)                                          %apertura trigger BIOPAC che viene dato a 0ms all'onset e dura 500ms;
    BIOPAC_aperto=1;
    if BIOPAC_aperto==1
        disp('TRIGGER --> BIOPAC Trigger ON');
    else
        disp('****BIOPAC Trigger-ON FAILED!!!');
    end
    
    %Image 2/4 - Show Context (DANGER) and ...
    context='context_danger.png';
    picture=imread(context);                                                %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,picture);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              

    %Image 3/4 - ... Show CS for 4s
    cs=(target_file);
    picture=imread(cs);                                                     %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,picture);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    disp('Show Context and CS (for 4s)');
    Screen('Flip',windowPtr);                                               %mostra l'immagine;
          
    startTime = GetSecs();

    %Regola la durata del Trial e TRIGGER BIOPAC
    keyIsDown=0;
    posizione=0;                
    pressed=0;
    time_pressed=0;
    time_end=0;
    
    while  time_off-time_on<=4                                              %definisce la durata massima del trial e in base al tempo regola i trigger;
       
       time_off=GetSecs();                                                 %cronometro: necessario per il while per capire quanto tempo Ë passato dall'onset;
       
       if time_off-time_on>=0.5 && BIOPAC_aperto==1;                        %definisce quando il BIOPAC deve essere chiuso (500ms dall'onset);    
       io64(ioObj,address_biopac,0);                              %chiusura trigger BIOPAC 500ms dopo essersi aperto;
       BIOPAC_aperto=0;                                 
           if BIOPAC_aperto==0
                disp('TRIGGER --> BIOPAC Trigger OFF');
           else
                disp('****BIOPAC Trigger-OFF FAILED!!!');
          end
       end
       
       %Reaction Time to CS and key's Release
       EnableKeys = RestrictKeysForKbCheck([32]);                           %Abilita solamente alcuni tasti da tastiera, in questo caso SPAZIO;
       [keyIsDown, pressedSecs, keyCode] = KbCheck();
       posizione=find(keyCode);
       
       if posizione==32
           time_end=GetSecs();         %key's release
       end
       
       if posizione==32 & pressed==0
            time_pressed=GetSecs();    %RT to CS
            pressed=1;
       end
             
    end %end while
    
    if pressed==1
       counter_RT_CS{counter}=time_pressed-startTime; 
       counter_keyrelease{counter}=(time_end-time_pressed);
       fprintf('\n RT= %.3f seconds\n',counter_RT_CS{counter});
       fprintf('\n Key''s Release= %.3f seconds\n\n',counter_keyrelease{counter});
    else 
       counter_RT_CS{counter}='missed';
       counter_keyrelease{counter}='missed';
       fprintf('\n    NON HA PREMUTO \n\n');
    end
    
    %Image 4/4 - Show Context (DANGER) for 1s after the CS
    context_ren='context_danger.png';
    context=imread(context_ren);                                            %legge l'immagine JPEG;
    texture = Screen('MakeTexture',windowPtr,context);                      %converte l'immagine in matrice;
    Screen('DrawTexture', windowPtr, texture);                              
    Screen('Flip',windowPtr);                                               %mostra l'immagine;
    disp('Show Context after the CS (for 1s)');
    WaitSecs(1);
    
    if j == 1
        counter_emiblocchi(sum(counter,counter_renewal))=1;
    else
        counter_emiblocchi(sum(counter,counter_renewal))=2;
    end
    
    counter_renewal=(counter_renewal+1);                                    %aggiornamento counter Renewal (tiene conto di quanti stim son stati presentati);
    counter_stim{counter}=target_file;                                      %aggiornamento counter stimoli (scrive che stimolo Ë stato presentato in questo trial);
    counter_context{counter}=context_ren;                                   %aggiornamento counter contesto (scrive che contesto Ë stato presentato in questo trial);
end

%% Function --> ITI
function ITI(windowPtr,rect)
global ioObj;
global address_biopac;
global address_shock;
global counter;

io64(ioObj,address_biopac,0);                                               %double check, che le porte parallele siano chiuse prima di un nuovo trial;
io64(ioObj,address_shock,0);                                                %double check, che le porte parallele siano chiuse prima di un nuovo trial;

Screen('FillRect', windowPtr, [125 125 125],rect);                          %fa comparire una schermata bianca di ITI;
Screen('Flip',windowPtr);

counter=counter+1;                                                          %aggiornamento del contatore che tiene conto degli items presentati dall'inizio del task alla fine;

ITI_time=randi([13,16],1);                                                  %regola la durata della schermata bianca di ITI, variabile tra 11 e 17s;
% ITI_time=randi([1,2],1);
fprintf('ITI di %d secondi',ITI_time);
WaitSecs(ITI_time);                                                         %durata dell'ITI; 
end

%% Function --> Partial Saving Emi-Block
function partial_saving
global nomefile;
global counter_sess;
global counter_emiblocchi;
global counter_CS;
global counter_stim;
global counter_context;
global counter_RT_CS;
global input_folder;
global output_folder;
global counter_keyrelease; 

cd(output_folder);                                                          %cambia percorso, posizionando l'output in una specifica cartella;

fprintf(' \n- - - - - - - - - - - - - - - - - - - - - - - - ');
fprintf('\n\n --> Saving Emi-Block Performance\n');

%Trasponi per salvataggio
counter_sess=counter_sess';
counter_emiblocchi=counter_emiblocchi';
counter_stim=counter_stim';
counter_CS=counter_CS';
counter_context=counter_context';
counter_RT_CS=counter_RT_CS';
counter_keyrelease=counter_keyrelease';
  
%Creazione file .excel parziale                                              
T = table(counter_sess,counter_emiblocchi,counter_CS,counter_stim,counter_context,counter_RT_CS,counter_keyrelease,...
  'VariableNames',{'Session','HemiBlock','CS_List','Stimulus','Context_List','RT_to_CS','KeyRelease'});             %crea una tabella dove inserisce i vari dati raccolti;
filename = nomefile;                                                                                   %crea il file excel se non esiste, LO SOVRASCRIVE se esiste
writetable(T,filename,'Sheet',1,'Range','A1')                                                          %inserisce la tabella (T) nell'excel foglio 1 partendo da A1;

%Trasponi per Matlab  
counter_sess=counter_sess';
counter_emiblocchi=counter_emiblocchi';
counter_stim=counter_stim';
counter_CS=counter_CS';
counter_context=counter_context';
counter_RT_CS=counter_RT_CS';
counter_keyrelease=counter_keyrelease';

cd(input_folder);   
end

function script_pause(windowPtr,rect)

%Define dot characteristics
crossLength = 3;
crossColor = 1; 
crossWidth = 4;

%Set start and end points of lines
crossLines = [-crossLength, 0; crossLength, 0; 0, -crossLength; 0, crossLength];
crossLines = crossLines';

%Define center of Screen
xCenter = rect(3)/2;
yCenter = rect(4)/2;

%Draw the dot
Screen('DrawLines',windowPtr,crossLines,crossWidth,crossColor,[xCenter,yCenter]);
Screen('Flip',windowPtr);
disp('--> PAUSE, press ''p'' to continue');

EnableKeys = RestrictKeysForKbCheck(80);                                    %Abilita solamente alcuni tasti da tastiera, in questo caso la 'P';
                                            %P per continuare                               
[secs, keyCode, deltaSecs] = KbWait();                                      %fin quando non preme un tasto della tastiera lo script non va avanti;
find(keyCode);                                                              %restituisce il tasto che ha premuto in codice;
KbName(keyCode);                                                            %restituisce quale tasto corrisponde a quel codice;

end
%% Function --> End-Block
function end_block(windowPtr)

Screen('TextSize',windowPtr,48);
Screen('TextFont',windowPtr,'Helvetica');
Screen('TextStyle',windowPtr,0);
DrawFormattedText(windowPtr,'Fine \n\n\n\n\n\n\n\n\n Premere la BARRA SPAZIATRICE per continuare\n','center','center',[0 0 0]); %fa comparire una schermata con la scritta fine blocco;
Screen('Flip',windowPtr);

fprintf('\n - - - - - - - - - - - - - - - - - - - - - - - -\n ');
disp('END BLOCK');
fprintf('\n - - - - - - - - - - - - - - - - - - - - - - - - ');

EnableKeys = RestrictKeysForKbCheck(32);                                    %Abilita solamente alcuni tasti da tastiera, in questo caso la BARRA SPAZIATRICE;

[secs, keyCode, deltaSecs] = KbWait();                                      %fin quando non preme un tasto della tastiera lo script non va avanti;
find(keyCode);                                                              %restituisce il tasto che ha premuto in codice;
KbName(keyCode); 
end

%% Function --> End-Scritp                                                  
function end_task(windowPtr)
global nomefile;
global counter_emiblocchi;
global counter_CS;
global counter_stim;
global counter_sess;
global counter_context;
global counter_RT_CS;
global output_folder;
global counter_keyrelease;

cd(output_folder);                                                          %cambia percorso, posizionando l'output in una specifica cartella;

Screen('TextSize',windowPtr,40);
Screen('TextFont',windowPtr,'Helvetica');
Screen('TextStyle',windowPtr,0);
DrawFormattedText(windowPtr,'Fine \n\n\n\n\n\n\n ATTENDERE che la schermata si chiuda automaticamente','center','center',[200 200 200]); %fa comparire una schermata che comunica che il task Ë stato completato;
Screen('Flip',windowPtr);
WaitSecs(1);                                                                %regola la durata della schermata di end-task;

fprintf('\n\n\nEND TASK');
fprintf(' - - - - - - - - - - - - - - - - - - - - - - - - ');
fprintf('\nSession Completed in \n');
toc;

%Trasposizione per salvataggio
counter_emiblocchi=counter_emiblocchi';
counter_CS=counter_CS';
counter_stim=counter_stim';
counter_sess=counter_sess';
counter_context=counter_context';
counter_RT_CS=counter_RT_CS';
counter_keyrelease=counter_keyrelease';

fprintf('\n--> Exporting data...\n\n');

%Creazione file .excel                                               
T = table(counter_sess,counter_emiblocchi,counter_CS,counter_stim,counter_context,counter_RT_CS,counter_keyrelease,...
  'VariableNames',{'Session','HemiBlock','CS_List','Stimulus','Context_List','RT_to_CS','KeyRelease'});  %crea una tabella dove inserisce i vari dati raccolti;
filename = nomefile;                                                                                    %crea il file excel se non esiste, LO SOVRASCRIVE se esiste
writetable(T,filename,'Sheet',1,'Range','A1')                                                           %inserisce la tabella (T) nell'excel foglio 1 partendo da A1;

%Creazione file .dat
fileDAT=strcat(nomefile,'.dat');
length_for=length(counter_CS);
fileID = fopen(fileDAT','wt+');
for k=1:length_for
   fprintf(fileID,'%s',strjoin(counter_CS(k)));
   fprintf(fileID,'\n');
end
fclose(fileID);

fprintf('- - - - - - - - - - - - - - - - - - - - - - - - - - - - -');
fprintf('\nData Exported in %s',output_folder);
fprintf('\nIl file EXCEL dal nome ''%s'' Ë stato generato correttamente',nomefile);
fprintf('\nIl file DAT dal nome ''%s.dat'' Ë stato generato correttamente',nomefile);
fprintf('\n- - - - - - - - - - - - - - - - - - - - - - - - - - - - -');
  
ShowCursor;                                                                 %fa ricomparire il cursore di Windows;
Screen('Close');                                                            %chiusura task;
Screen('CloseAll');                                                         %chiusura task;
end
