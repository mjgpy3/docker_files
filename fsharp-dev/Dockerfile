FROM fsharp

# Install some tools for dev
RUN apt-get update && apt-get install vim git -y

# Install my vim dotfiles
RUN git clone https://github.com/mjgpy3/dotfiles.git /tmp/dotfiles && \
    mv /tmp/dotfiles/vimrc ~/.vimrc

# Install Pathogen & plugins
RUN mkdir -p ~/.vim/autoload ~/.vim/bundle && curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim && \
    git clone https://github.com/fsharp/vim-fsharp.git ~/.vim/bundle/vim-fsharp && \
    cd ~/.vim/bundle/vim-fsharp && apt-get install unzip && make && \
    git clone https://github.com/kien/ctrlp.vim.git ~/.vim/bundle/ctrlp.vim

# Make some important directories
RUN mkdir -p ~/.vim/backup ~/.vim/tmp /app /root/.ssh

WORKDIR /app

VOLUME /app
VOLUME /root/.ssh

ENTRYPOINT ["vim"]
