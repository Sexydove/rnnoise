cd ~/project/rnnoise
make distclean
./autogen.sh
./configure
cd ~/project/rnnoise/src
./compile.sh
cd ~/project/rnnoise
~/project/rnnoise/src/denoise_training ~/project/noise_cancel/speech_only.pcm ~/project/noise_cancel/noise_only.pcm output.f32
python3 ~/project/rnnoise/training/bin2hdf5.py output.f32 500000 87 denoise_data9.h5
~/project/rnnoise/training/dump_rnn.py newweights9i.hdf5 rnn_data.c rnn_data.h
python3 ~/project/rnnoise/training/dump_rnn.py newweights9i.hdf5 ./src/rnn_data.c ./src/rnn_data.h
~/project/rnnoise/examples/rnnoise_demo ../noise_cancel/speech_noise.pcm ./denoised_speech_noise.pcm
~/project/wavutils/bin/pcm2wav 1 48000 16 ~/project/wavutils/denoised_speech_noise.pcm ~/project/wavutils/denoised_speech_noise.wav

~/project/rnnoise
