# Copyright 2025 The Sigstore Authors
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# optionally set these env variables
FULCIO_REPO ?= https://github.com/sigstore/fulcio.git
REKOR_REPO ?= https://github.com/sigstore/rekor.git
REKORV2_REPO ?= https://github.com/sigstore/rekor-tiles.git
TIMESTAMP_REPO ?= https://github.com/sigstore/timestamp-authority.git

# prevent a conflict with rekor-server's metrics port.
export FULCIO_METRICS_PORT = 2113
export FULCIO_CONFIG = $(PWD)/fulcio_config.json

CHECKOUT_DIR ?= ./CHECKOUT_DIR
FULCIO_DIR ?= $(CHECKOUT_DIR)/fulcio
REKOR_DIR ?= $(CHECKOUT_DIR)/rekor
REKORV2_DIR ?= $(CHECKOUT_DIR)/rekorv2
TIMESTAMP_DIR ?= $(CHECKOUT_DIR)/timestamp
FAKEOIDC_DIR = fakeoidc

.PHONY: checkout
checkout:
# checkout the repos locally.
ifeq ($(wildcard $(FULCIO_DIR)),)
	git clone --depth 1 $(FULCIO_REPO) $(FULCIO_DIR)
else
	@echo "Already cloned fulcio"
endif
ifeq ($(wildcard $(REKOR_DIR)),)
	git clone --depth 1 $(REKOR_REPO) $(REKOR_DIR)
else
	@echo "Already cloned rekor"
endif
ifeq ($(wildcard $(REKORV2_DIR)),)
	git clone --depth 1 $(REKORV2_REPO) $(REKORV2_DIR)
else
	@echo "Already cloned rekorv2"
endif
ifeq ($(wildcard $(TIMESTAMP_DIR)),)
	git clone --depth 1 $(TIMESTAMP_REPO) $(TIMESTAMP_DIR)
else
	@echo "Already cloned timestamp"
endif

# fulcio

.PHONY: build-fulcio
build-fulcio:
	cd $(FULCIO_DIR) && docker compose build

.PHONY: up-fulcio
up-fulcio:
	cd $(FULCIO_DIR) && docker compose up --wait

.PHONY: down-fulcio
down-fulcio:
	cd $(FULCIO_DIR) && docker compose down

# rekor

.PHONY: build-rekor
build-rekor:
	cd $(REKOR_DIR) && docker compose build

.PHONY: up-rekor
up-rekor:
	cd $(REKOR_DIR) && docker compose up --wait

.PHONY: down-rekor
down-rekor:
	cd $(REKOR_DIR) && docker compose down

# rekorv2

.PHONY: build-rekorv2
build-rekorv2:
	cd $(REKORV2_DIR) && docker compose build

.PHONY: up-rekorv2
up-rekorv2:
	cd $(REKORV2_DIR) && docker compose up --wait

.PHONY: down-rekorv2
down-rekorv2:
	cd $(REKORV2_DIR) && docker compose down

# timestamp

.PHONY: build-timestamp
build-timestamp:
	cd $(TIMESTAMP_DIR) && docker compose build

.PHONY: up-timestamp
up-timestamp:
	cd $(TIMESTAMP_DIR) && docker compose up --wait

.PHONY: down-timestamp
down-timestamp:
	cd $(TIMESTAMP_DIR) && docker compose down

# fakeoidc

.PHONY: build-fakeoidc
build-fakeoidc:
	cd $(FAKEOIDC_DIR) && docker compose build

.PHONY: up-fakeoidc
up-fakeoidc:
	cd $(FAKEOIDC_DIR) && docker compose up --wait

.PHONY: down-fakeoidc
down-fakeoidc:
	cd $(FAKEOIDC_DIR) && docker compose down
