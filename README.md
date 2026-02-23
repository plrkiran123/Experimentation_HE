# Experimentation_HE

Pull openfhe development
integrate these files into openfhe development
run server/python3 app.py
run client
plrkiran@macbookair-1 client % g++ -std=c++17 encryption.cpp -o encryption \
  -I/usr/local/include/openfhe \
  -I/usr/local/include/openfhe/core \
  -I/usr/local/include/openfhe/pke \
  -I/usr/local/include/openfhe/binfhe \
  -I/opt/homebrew/Cellar/nlohmann-json/3.11.3/include \
  -L/usr/local/lib -lOPENFHEcore -lOPENFHEpke -lOPENFHEbinfhe -lcurl \
  -Wl,-rpath,/usr/local/lib

g++ -std=c++17 clustering.cpp -o clustering \
  -I/usr/local/include/openfhe \
  -I/usr/local/include/openfhe/core \
  -I/usr/local/include/openfhe/pke \
  -I/usr/local/include/openfhe/binfhe \
  -I/opt/homebrew/Cellar/nlohmann-json/3.11.3/include \
  -L/usr/local/lib -lOPENFHEcore -lOPENFHEpke -lOPENFHEbinfhe -lcurl \
  -Wl,-rpath,/usr/local/lib

./encryption
./clustering


# Parameter Mapping to Thesis Table 5.2

| Thesis Parameter | Code Location | Example Values Used |
|---|---|---|
| Ring Dim $N$ | `src/main.cpp:130` | 8192, 16k, 32k |
| Mult Depth $L$ | `config/params.yaml` | 3,4,6,10 |
| Batch Size | `src/packing.cpp:45` | 1024, 4096, 16384 |
| Scale | `src/ckks.cpp:89` | $2^{40}$ (40 bits) |

# Reproduce Table 6.4 Results
```bash
cd HE
python scripts/run_kmeans.py --n 1e6 --k 8 --N 16384 --depth 4 --scale 40 --batch 4096
