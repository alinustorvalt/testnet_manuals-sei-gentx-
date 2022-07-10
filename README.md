# testnet_manuals/sei/gentx/

## Generate Gentx for Sei Incentivized testnet

 Setting up vars
 
 
 
 

Di sini Anda harus memasukkan nama moniker Anda (validator) yang akan terlihat di explorer

> NODENAME=<YOUR_MONIKER_NAME_GOES_HERE>


Simpan dan impor variabel ke dalam sistem

> echo "export NODENAME=$NODENAME" >> $HOME/.bash_profile echo "export WALLET=wallet" >> $HOME/.bash_profile echo "export CHAIN_ID=atlantic-1" >> $HOME/.bash_profile source $HOME/.bash_profile


Perbarui paket

> sudo apt update && sudo apt upgrade -y


Instal dependensi

> sudo apt-get install make build-essential gcc git jq chrony -y


Install go

> ver="1.18.2" cd $HOME wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz" sudo rm -rf /usr/local/go sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz" rm "go$ver.linux-amd64.tar.gz" echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> ~/.bash_profile source ~/.bash_profile


Unduh dan instal binari

> cd $HOME git clone https://github.com/sei-protocol/sei-chain.git && cd $HOME/sei-chain git checkout 1.0.6beta make install


Config app

> seid config chain-id $CHAIN_ID seid config keyring-backend test


Init node

> seid init $NODENAME --chain-id $CHAIN_ID


Pulihkan atau buat dompet baru untuk testnet Berinsentif ! Jika Anda membuat dompet baru, jangan lupa untuk menuliskan mnemonic 12 kata Anda!

Opsi 1 - hasilkan dompet baru
> seid keys add $WALLET

Opsi 2 - pulihkan dompet yang ada
> seid keys add $WALLET --recover


Tambahkan akun genesis

> WALLET_ADDRESS=$(seid keys show $WALLET -a) seid add-genesis-account $WALLET_ADDRESS 10000000usei



Hasilkan gentx Silakan isi <your_validator_description>, <your_email> dan <your_website> dengan nilai Anda sendiri

> seid gentx $WALLET 10000000usei
> --chain-id $CHAIN_ID
> --moniker=$NODENAME
> --commission-max-change-rate=0.01
> --commission-max-rate=0.20
> --commission-rate=0.05
> --details="<your_validator_description>"
> --security-contact="<your_email>"
> --website="<your_website>"


Hal-hal yang harus Anda backup

12 kata mnemonik dari dompet yang Anda buat
isi dari $HOME/.sei/config/*
Kirim PR dengan Gentx

1.Salin konten $HOME/.sei/config/gentx/gentx-XXXXXXX.json 
2.Fork https://github.com/sei-protocol/testnet 
3.Buat file gentx-{VALIDATOR_NAME}.json di bawah folder testnet/sei-incentivized-testnet/gentx di repo bercabang, tempel teks yang disalin ke dalam file. 
4.Buat Permintaan Tarik ke cabang utama repositori

# Tunggu instruksi selanjutnya!
0 comments on commit 82ace59
