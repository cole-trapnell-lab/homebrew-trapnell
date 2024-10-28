# Customizable R Homebrew formula for accelerated linear algebra

This is a custom Homebrew R formula that enables OpenBLAS and OpenMP for accelerated linear algebra. It does not require X11/XQuartz and instead relies on Cairo for graphics support. It includes dependencies listed in [this blog post](https://www.btskinner.io/code/install-r-with-openblas-and-openmp-on-macos-mojave/) by Benjamin T. Skinner and is based on [this discussion](https://github.com/sethrfore/homebrew-r-srf/pull/61) with Seth R. Fore.

This formula has only been tested on MacOS. It is based off of the Homebrew core formula, so it should work on other systems, but it has not been tested. Install at your own risk.

## Installation

This modified R formula can be installed as follows.

Add the repository to your homebrew
```sh
brew tap cole-trapnell-lab/homebrew-trapnell
```

Compile the modified R formula from source:

```sh
brew install -s cole-trapnell-lab/homebrew-trapnell/r
```

You should also install the `cmake` cask so you can install some R packages:

```sh
brew install --cask cmake
```

Check if the default R is correct by running `which R`. It should be `$(brew --prefix)/bin/R`, e.g. `/opt/homebrew/bin/R`. You might have to start a new terminal session for it to take effect. 

Once installed, the compiled dependencies can be checked by invoking R and running `capabilities()`. You can test if everything is as expected with the following:
```r
all(capabilities == c(jpeg = TRUE,
					  png = TRUE,
					  tiff = TRUE,
					  tcltk = FALSE,
					  X11 = FALSE,
					  aqua = TRUE,
					  `http/ftp` = TRUE,
					  sockets = TRUE,
					  libxml = FALSE,
					  fifo = TRUE,
					  cledit = TRUE,
					  iconv = TRUE,
					  NLS = TRUE,
					  Rprof = TRUE,
					  profmem = TRUE,
					  cairo = TRUE,
					  ICU = TRUE,
					  long.double = FALSE,
					  libcurl = TRUE)
)
```

If the result of the above is not TRUE, check the individual `capabilities()`:
```r
       jpeg         png        tiff       tcltk         X11        aqua
       TRUE        TRUE        TRUE       FALSE       FALSE        TRUE
   http/ftp     sockets      libxml        fifo      cledit       iconv
       TRUE        TRUE       FALSE        TRUE        TRUE        TRUE
        NLS       Rprof     profmem       cairo         ICU long.double
       TRUE        TRUE        TRUE        TRUE        TRUE       FALSE
    libcurl
       TRUE
```

Once the capabilities are properly set, you can safely uninstall previous versions of R. You may have to reinstall your R libraries.

## Contributing

We cannot provide support for this formula and cannot help troubleshoot any installation issues. However, we welcome any contributions to this formula; if you would like to contribute, please open a pull request.