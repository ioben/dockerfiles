FROM archlinux as rua_builder

WORKDIR /tmp
RUN useradd -m builder

RUN pacman -Sy && \
    pacman --noconfirm -S gcc awk git sudo file binutils fakeroot rustup bubblewrap

USER builder

RUN git clone https://aur.archlinux.org/rua.git && \
    cd rua && \
    makepkg


FROM archlinux
COPY --from=rua_builder /tmp/rua/rua*.pkg.tar.xz /tmp
RUN pacman --noconfirm -Syu && \
    pacman --noconfirm -S git bubblewrap && \
    pacman --noconfirm -U /tmp/rua*.pkg.tar.xz && \
    rm /tmp/*.pkg.tar.xz