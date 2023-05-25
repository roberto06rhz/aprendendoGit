# aprendendoGit
oie
import React, { useEffect, useState } from 'react';
import { Link, useParams } from 'react-router-dom';

import './DetalheProdutoInformatica.css';

function DetalheProdutoInformatica() {
    const { id } = useParams();
    const [produto, setProduto] = useState(null);

    useEffect(() => {
        const loadProduto = async () => {
            const result = await fetch(`https://dummyjson.com/products/${id}`);
            const p = await result.json();

            setProduto({
                id: p.id,
                nome: p.title,
                marca: p.brand,
                preco: p.price,
                avaliacao: p.rating,
                estoque: p.stock,
                categoria: p.category,
                img: p.thumbnail,
                img1: p.images[2],
                img2: p.images[3],
                descricao: p.description
            });
        };

        loadProduto();
    }, [id]);

    return (
        <div className='containerInformaticaDetalhes'>
            <h2>Detalhes do produto ID: {id}</h2>
            {
            
                <div className='telaInformaticaCardDetalhes'>

                    <div className='telaInformaticaImgDetalhes' >
                        <img className='img' src={produto?.img}></img>
                        <img className='img' src={produto?.img1}></img>
                        <img className='img' src={produto?.img2}></img>
                       
                    </div>

                    <div className='textoDetalhes' >
                        Modelo: <span className='textoPDetalhes'>{produto?.nome}</span>
                    </div>
                    <div className='textoDetalhes' >
                        Marca: <span className='textoPDetalhes'>{produto?.marca}</span>
                    </div>
                    <div className='textoDetalhes' >
                        Descrição: <span className='textoPDetalhes'>{produto?.descricao}</span>
                    </div>
                    <div className='textoDetalhes'>
                        Preço: <span className='textoPDetalhes'>${produto?.preco}</span>
                    </div>
                    <div className='textoDetalhes'>
                        Quantidade Disponivel: <span className='textoPDetalhes'>{produto?.estoque}</span>
                    </div>
                    <div className='textoDetalhes'>
                        Avaliação: <span className='textoPDetalhes'>{produto?.avaliacao}</span>
                    </div>
                </div>
            }
            <h3><Link to="/informatica">Retornar Ao setor Informatica</Link></h3>
        </div>
    );
}                        

export default DetalheProdutoInformatica;
