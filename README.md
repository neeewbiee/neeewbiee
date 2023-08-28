ChannelID = 2248809;
ReadAPIKey = 'GAGQKZ08OAM1ZQBN';

LDRData01 = thingSpeakRead(ChannelID, ...
    ReadKey = ReadAPIKey, ...
    OutputFormat = 'timetable', ...
    Fields = [1:4], ...
    DateRange = [datetime('2020-01-01'),datetime('2020-02-01')] ...
    );

LDRData02 = thingSpeakRead(ChannelID, ...
    ReadKey = ReadAPIKey, ...
    OutputFormat = 'timetable', ...
    Fields = [1:4], ...
    DateRange = [datetime('2020-02-01'),datetime('2020-03-01')] ...
    );

LDRData03 = thingSpeakRead(ChannelID, ...
    ReadKey = ReadAPIKey, ...
    OutputFormat = 'timetable', ...
    Fields = [1:4], ...
    DateRange = [datetime('2020-03-01'),datetime('2020-04-01')] ...
    );

LDRData04 = thingSpeakRead(ChannelID, ...
    ReadKey = ReadAPIKey, ...
    OutputFormat = 'timetable', ...
    Fields = [1:4], ...
    DateRange = [datetime('2020-04-01'),datetime('2020-05-01')] ...
    );

LDRData05 = thingSpeakRead(ChannelID, ...
    ReadKey = ReadAPIKey, ...
    OutputFormat = 'timetable', ...
    Fields = [1:4], ...
    DateRange = [datetime('2020-05-01'),datetime('2020-06-01')] ...
    );

LDRData06 = thingSpeakRead(ChannelID, ...
    ReadKey = ReadAPIKey, ...
    OutputFormat = 'timetable', ...
    Fields = [1:4], ...
    DateRange = [datetime('2020-06-01'),datetime('2020-07-01')] ...
    );

LDRData07 = thingSpeakRead(ChannelID, ...
    ReadKey = ReadAPIKey, ...
    OutputFormat = 'timetable', ...
    Fields = [1:4], ...
    DateRange = [datetime('2020-07-01'),datetime('2020-08-01')] ...
    );

LDRData08 = thingSpeakRead(ChannelID, ...
    ReadKey = ReadAPIKey, ...
    OutputFormat = 'timetable', ...
    Fields = [1:4], ...
    DateRange = [datetime('2020-08-01'),datetime('2020-09-01')] ...
    );

LDRData09 = thingSpeakRead(ChannelID, ...
    ReadKey = ReadAPIKey, ...
    OutputFormat = 'timetable', ...
    Fields = [1:4], ...
    DateRange = [datetime('2020-09-01'),datetime('2020-10-01')] ...
    );

LDRData10 = thingSpeakRead(ChannelID, ...
    ReadKey = ReadAPIKey, ...
    OutputFormat = 'timetable', ...
    Fields = [1:4], ...
    DateRange = [datetime('2020-10-01'),datetime('2020-11-01')] ...
    );

LDRData11 = thingSpeakRead(ChannelID, ...
    ReadKey = ReadAPIKey, ...
    OutputFormat = 'timetable', ...
    Fields = [1:4], ...
    DateRange = [datetime('2020-11-01'),datetime('2020-12-01')]...
    );

LDRData12 = thingSpeakRead(ChannelID, ...
    ReadKey = ReadAPIKey, ...
    OutputFormat = 'timetable', ...
    Fields = [1:4], ...
    DateRange = [datetime('2020-12-01'),datetime('2021-01-01')] ...
    );

LDRDataFull = [LDRData01; LDRData02; LDRData03; LDRData04; LDRData05; ...
              LDRData06; LDRData07; LDRData08; LDRData09; LDRData10; ...
              LDRData11; LDRData12];

display(size(LDRDataFull),'Size of full dataset');
          
LDRDataFull.Properties.VariableNames{1} = 'Day';
LDRDataFull.Properties.VariableNames{2} = 'Location';
LDRDataFull.Properties.VariableNames{3} = 'Voltage';
LDRDataFull.Properties.VariableNames{4} = 'relay';

LDRDataFull.Voltage = string(LDRDataFull.Voltage);
BadDatas = ismissing(LDRDataFull.Voltage,{'Nan' 'nan' 'na' 'N.A' ''});
display(head(LDRDataFull(BadDatas,:)),'Bad datas');
LDRDataFull(BadDatas,:) = [];  % Delete rows from the entire table

LDRDataFull.Voltage = double(LDRDataFull.Voltage);

outlierRows = isoutlier(LDRDataFull.Voltage, 'mean');
outliers = LDRDataFull.Voltage(outlierRows,:);
display(head(LDRDataFull(outlierRows,:)),'outlier');
LDRDataFull(outlierRows,:) = [];

LDRDataFull.Light = (LDRDataFull.Voltage/5)*1024;

%Location
FHData = LDRDataFull;
MLData = LDRDataFull;
L1Data = LDRDataFull;
L2Data = LDRDataFull;
L3Data = LDRDataFull;
L4Data = LDRDataFull;

FHData.Location = string(FHData.Location);
unwantedData = find(FHData.Location ~= 'FH');
FHData(unwantedData,:) = [];
head(FHData);

MLData.Location = string(MLData.Location);
unwantedData = find(MLData.Location ~= 'ML');
MLData(unwantedData,:) = [];
head(MLData);

L1Data.Location = string(L1Data.Location);
unwantedData = find(L1Data.Location ~= 'L1');
L1Data(unwantedData,:) = [];
head(L1Data);

L2Data.Location = string(L2Data.Location);
unwantedData = find(L2Data.Location ~= 'L2');
L2Data(unwantedData,:) = [];
head(L2Data);

L3Data.Location = string(L3Data.Location);
unwantedData = find(L3Data.Location ~= 'L3');
L3Data(unwantedData,:) = [];
head(L3Data);

L4Data.Location = string(L4Data.Location);
unwantedData = find(L4Data.Location ~= 'L4');
L4Data(unwantedData,:) = [];
head(L4Data);

%Day
monData = LDRDataFull;
tueData = LDRDataFull;
wedData = LDRDataFull;
thuData = LDRDataFull;
friData = LDRDataFull;
satData = LDRDataFull;
sunData = LDRDataFull;

%monData = string(FHData.Location);
monData.Day = string(monData.Day)
unwantedData = find(monData.Day ~= 'Mon');
monData(unwantedData,:) = [];

tueData.Day = string(tueData.Day)
unwantedData = find(tueData.Day ~= 'Tue');
tueData(unwantedData,:) = [];

wedData.Day = string(wedData.Day)
unwantedData = find(wedData.Day ~= 'Wed');
wedData(unwantedData,:) = [];

thuData.Day = string(thuData.Day)
unwantedData = find(thuData.Day ~= 'Thu');
thuData(unwantedData,:) = [];

friData.Day = string(friData.Day)
unwantedData = find(friData.Day ~= 'Fri');
friData(unwantedData,:) = [];

satData.Day = string(satData.Day)
unwantedData = find(satData.Day ~= 'Sat');
satData(unwantedData,:) = [];

sunData.Day = string(sunData.Day)
unwantedData = find(sunData.Day ~= 'Sun');
sunData(unwantedData,:) = [];

% Calculate average light values for each location and day

monMean = mean([FHData.Light, MLData.Light, L1Data.Light, L2Data.Light, L3Data.Light, L4Data.Light], 2);
tueMean = mean([FHData.Light, MLData.Light, L1Data.Light, L2Data.Light, L3Data.Light, L4Data.Light], 2);
wedMean = mean([FHData.Light, MLData.Light, L1Data.Light, L2Data.Light, L3Data.Light, L4Data.Light], 2);
thuMean = mean([FHData.Light, MLData.Light, L1Data.Light, L2Data.Light, L3Data.Light, L4Data.Light], 2);
friMean = mean([FHData.Light, MLData.Light, L1Data.Light, L2Data.Light, L3Data.Light, L4Data.Light], 2);
satMean = mean([FHData.Light, MLData.Light, L1Data.Light, L2Data.Light, L3Data.Light, L4Data.Light], 2);
sunMean = mean([FHData.Light, MLData.Light, L1Data.Light, L2Data.Light, L3Data.Light, L4Data.Light], 2);

% Combine mean values for each location and day
meanValues = [monMean, tueMean, wedMean, thuMean, friMean, satMean, sunMean];

% Bar plot
BarLabels = categorical({'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'});
DesiredOrder = {'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'};
BarLabels = reordercats(BarLabels, DesiredOrder);

% Create a bar plot for mean light values
bar(BarLabels, meanValues, 'grouped');
