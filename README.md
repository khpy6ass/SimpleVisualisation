# SimpleVisualisation
An outline script that allows image display in fMRI data
% 
% AS 2020-03-06. dafni class session 6

%% Preliminiary
%
% commands and functions we need to remember. 
% 1. load in the nifti file. 
% 1a. niftiinfo()
% 1b. niftiread()

% also: really interesting looking function for displaying 3d data in
% volumeViewer()

% 2 displaying images
% 
% image() axis/image orientation
% imagesc() % display intensity images with weird ranges
%
% returnSlice() % from previous work might be useful 

%% Plan for Montage
%
% Given 3d array data
% How to display montage()
% Change which images/slices are being displayed
% How to change the range colors that are being display 

% - 1. Make some data (random numbers, 3D array, whether matlab has a dataset
% built-in for use. 
% - 2. matlab some built-in data sets....

% load MRI % load the data set that TMS gives us

% convert the 4d dataset into 3D

% D_3d = squeeze(D);

%% Load an actual data set from class (niftiread)

fname = '~/data/subject-C/mprage.nii.gz';

data = niftiread(fname);

montage(data);

%%
nSlices = size(data, 3);
nDisplay = 25; 
idx= round( linspace(1, nSlices, nDisplay)); % nice numbers 

montage(data, 'indices', idx);

%% Now fix display range 

% find 5 and 9th percentile that gives a better value for LOW and HIGH
% points in color map. 

robustRange = prctile(data(:), [5, 95]);
montage(data, 'indices', idx, 'Displayrange', robustRange);

%% Weird Orientation- can we change the dimension
%
% Idea is permute dims

dataP = permute(data, [2, 1, 3]); % To change the 1st dimension to the 2nd dimension, and the 2nd dimension as the 1st dimension. 

montage(dataP, 'indices', idx, 'Displayrange', robustRange);

%% End of Documentation
