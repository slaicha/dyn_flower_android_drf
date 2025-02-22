# dyn_flower_android_drf

Dynamic Flower model use on Android by wrapping Flower with Django REST Framework

Please see `backend/README.md` for information on how to set up the backend server, see `client/README.md` to set up the client.

---

Original README from Flower Android example:

# Flower Android Example (TensorFlowLite)

This example demonstrates a federated learning setup with Android Clients. The training on Android is done on a CIFAR10 dataset using TensorFlow Lite. The setup is as follows:

- The CIFAR10 dataset is randomly split across 10 clients. Each Android client holds a local dataset of 5000 training examples and 1000 test examples.
- The FL server runs in Python but all the clients run on Android.
- We use a strategy called FedAvgAndroid for this example.
- The strategy is vanilla FedAvg with a custom serialization and deserialization to handle the Bytebuffers sent from Android clients to Python server.

## Project Setup

Start by cloning the example project. We prepared a single-line command that you can copy into your shell which will checkout the example for you:

```shell
git clone --depth=1 https://github.com/adap/flower.git && mv flower/examples/android . && rm -rf flower && cd android
```

Project dependencies (such as `tensorflow` and `flwr`) are defined in `pyproject.toml`. We recommend [Poetry](https://python-poetry.org/docs/) to install those dependencies and manage your virtual environment ([Poetry installation](https://python-poetry.org/docs/#installation)), but feel free to use a different way of installing dependencies and managing virtual environments if you have other preferences.

```shell
poetry install
poetry shell
```

Poetry will install all your dependencies in a newly created virtual environment. To verify that everything works correctly you can run the following command:

```shell
poetry run python3 -c "import flwr"
```

If you don't see any errors you're good to go!

# Run Federated Learning on Android Devices

The included `run.sh` will start the Flower server (using `server.py`). You can simply start it in a terminal as follows:

```shell
poetry run ./run.sh
```

Download and install the `flwr_android_client.apk` on each Android device/emulator. The server currently expects a minimum of 4 Android clients, but it can be changed in the `server.py`.

When the Android app runs, add the client ID (between 1-10), the IP and port of your server, and press `Load Dataset`. This will load the local CIFAR10 dataset in memory. Then press `Setup Connection Channel` which will establish connection with the server. Finally, press `Train Federated!` which will start the federated training.
