<div class="title" align=center>
    <h1>ProLigGPT</h1>
	<div>A GPT-based Strategy for Designing Potential Ligands Targeting Specific Proteins</div>
    <br/>
    <p>
        <img src="https://img.shields.io/github/license/LIYUESEN/ProLigGPT">
    	<img src="https://img.shields.io/badge/python-3.8-blue">
	<a href="https://colab.research.google.com/drive/1lxDpEGz9498tGvEi7nSgryXI4haMKMhc">
	<img src="https://colab.research.google.com/assets/colab-badge.svg"></a>
        <img src="https://img.shields.io/github/stars/LIYUESEN/ProLigGPT?style=social">
</div>

## 🚩 Introduction
ProLigGPT presents a ligand design strategy based on the autoregressive model, GPT, focusing on chemical space exploration and the discovery of ligands for specific proteins. Deep learning language models have shown significant potential in various domains including protein design and 
biomedical text analysis, providing strong support for the proposition of ProLigGPT. 

In this study, we employ the ProLigGPT model to learn a substantial amount of protein-ligand binding data, aiming to discover novel molecules that can bind with specific proteins. This strategy not only significantly improves the efficiency of ligand design but also offers a swift and effective avenue for the drug development process, bringing new possibilities to the pharmaceutical domain.
## 💽 System requirements
### OS requirements
This project is developed for Microsoft Windows and Linux, and has been tested on the following systems:
- **Microsoft Windows:** Windows 10 22H2
- **Linux:** Ubuntu 24.04 LTS
- **Google Colab**
### GPU computation platform requirements
This project has been tested on `CUDA 11.7.0` and `cuDNN 8`.
### Python dependencies
```
datasets==3.1.0
psutil==7.0.0
scikit-learn==1.3.2
scipy==1.10.1
transformers==4.46.3

conda-forge/label/cf202003::openbabel
```
## 📥 Installation guide
### Clone
```shell
git clone https://github.com/LIYUESEN/ProLigGPT.git
cd ProLigGPT
```
> Or you can just click *Code>Download ZIP* to download this repo.
### Create Python virtual environment (Take Conda as example)
```shell
conda create -n proliggpt python=3.8
conda activate proliggpt
```
### Install PyTorch and other requirements
```shell
pip install torch --index-url https://download.pytorch.org/whl/cu117
pip install datasets==3.1.0 transformers==4.46.3 scipy==1.10.1 scikit-learn==1.3.2 psutil==7.0.0
conda install conda-forge/label/cf202003::openbabel
```

> On Colab, the deployment process for this project took approximately **5 min**.
## 🗝 How to use
### 💻 Run in command
Use [proliggpt.py](https://github.com/LIYUESEN/ProLigGPT/blob/main/proliggpt.py)

Required parameters:
- `-p` | `--pro_seq`: Input a protein amino acid sequence.
- `-f` | `--fasta`: Input a FASTA file including one protein amino acid sequence.

  > Only one of -p and -f should be specified.
- `-l` | `--ligand_prompt`: Input a ligand prompt.
- `-n` | `--number`: The expected number of molecules to be generated.
- `-d` | `--device`: Hardware device to be used. Default is 'cuda'.
- `-o` | `--output`: Output directory for generated molecules. Default is './ligand_output/'.
- `-b` | `--batch_size`: The number of molecules to be generated per batch. Try to reduce this value if you have low RAM. Default is 16.
- `-t` | `--temperature`: Adjusts the randomness of text generation; higher values produce more diverse outputs. Default is 1.0.
- `--top_k`: The number of highest probability tokens to be considered for top-k sampling. Default is 9.
- `--top_p`: The cumulative probability threshold (0.0 - 1.0) for top-p (nucleus) sampling. It defines the minimum subset of tokens to consider for random sampling. Default is 0.9.
- `--min_atoms`: Minimum number of non-H atoms allowed for generation. Default is None.
- `--max_atoms`: Maximum number of non-H atoms allowed for generation. Default is 35.
- `--no_limit`: Disable the default max atoms limit.

  > If the `-l` | `--ligand_prompt` option is used, the `--max_atoms` and `--min_atoms` parameters will be disregarded.

### 🌎 Run in Google Colab
[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1lxDpEGz9498tGvEi7nSgryXI4haMKMhc)

The Colab notebook contains detailed usage instructions.
## 🔬 Example usage 
- If you want to input a protein FASTA file
    ```shell
    python proliggpt.py -f PK3CA.fasta -n 50
    ```
- If you want to input the amino acid sequence of the protein
    ```shell
    python proliggpt.py -p MPPRPSSGELWGIHLMPPRILVECLLPNGMIVTLECLREATLITIKHELFKEARKYPLHQLLQDESSYIFVSVTQEAEREEFFDETRRLCDLRLFQPFLKVIEPVGNREEKILNREIGFAIGMPVCEFDMVKDPEVQDFRRNILNVCKEAVDLRDLNSPHSRAMYVYPPNVESSPELPKHIYNKLDKGQIIVVIWVIVSPNNDKQKYTLKINHDCVPEQVIAEAIRKKTRSMLLSSEQLKLCVLEYQGKYILKVCGCDEYFLEKYPLSQYKYIRSCIMLGRMPNLMLMAKESLYSQLPMDCFTMPSYSRRISTATPYMNGETSTKSLWVINSALRIKILCATYVNVNIRDIDKIYVRTGIYHGGEPLCDNVNTQRVPCSNPRWNEWLNYDIYIPDLPRAARLCLSICSVKGRKGAKEEHCPLAWGNINLFDYTDTLVSGKMALNLWPVPHGLEDLLNPIGVTGSNPNKETPCLELEFDWFSSVVKFPDMSVIEEHANWSVSREAGFSYSHAGLSNRLARDNELRENDKEQLKAISTRDPLSEITEQEKDFLWSHRHYCVTIPEILPKLLLSVKWNSRDEVAQMYCLVKDWPPIKPEQAMELLDCNYPDPMVRGFAVRCLEKYLTDDKLSQYLIQLVQVLKYEQYLDNLLVRFLLKKALTNQRIGHFFFWHLKSEMHNKTVSQRFGLLLESYCRACGMYLKHLNRQVEAMEKLINLTDILKQEKKDETQKVQMKFLVEQMRRPDFMDALQGFLSPLNPAHQLGNLRLEECRIMSSAKRPLWLNWENPDIMSELLFQNNEIIFKNGDDLRQDMLTLQIIRIMENIWQNQGLDLRMLPYGCLSIGDCVGLIEVVRNSHTIMQIQCKGGLKGALQFNSHTLHQWLKDKNKGEIYDAAIDLFTRSCAGYCVATFILGIGDRHNSNIMVKDDGQLFHIDFGHFLDHKKKKFGYKRERVPFVLTQDFLIVISKGAQECTKTREFERFQEMCYKAYLAIRQHANLFINLFSMMLGSGMPELQSFDDIAYIRKTLALDKTEQEALEYFMKQMNDAHHGGWTTKMDWIFHTIKQHALN -n 50
    ```
    
- If you want to provide a prompt for the ligand  
    ```shell
    python proliggpt.py -f PK3CA.fasta -l CC1=C(SC(=N1)NC(=O)N2CCCC2C(=O)N) -n 50
    ```
    
- Note: If you are running in a Linux environment, you need to enclose the ligand's prompt with single quotes ('').  
    ```shell
    python proliggpt.py -f PK3CA.fasta -l 'CC1=C(SC(=N1)NC(=O)N2CCCC2C(=O)N)' -n 50
    ```
> On Colab, the generation process for 50 molecules took approximately **7 min**.
## 🌌 Model Visualization
[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1HUioWgOmVxmoP__sl-9qbyFlWajCdTHa)

We visualized the model's attention weights using [BertViz](https://github.com/jessevig/bertviz), illustrating clearly how ProLigGPT directly leverages input token information.
## ✉️ Contact
Yuesen Li      lisen2286@gmail.com  

Yungang Xu     yungang.xu@xjtu.edu.cn

## 📝 How to cite this work
TODO

## ⚖ License
[GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.html)
