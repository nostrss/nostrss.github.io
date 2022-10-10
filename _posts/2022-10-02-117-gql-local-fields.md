---
layout: post
title: '[Apollo-Client] Local-only fields '
author: 'Nostrss'
comments: true
tags: apollo client local only fields
excerpt_separator:
sticky:
hidden:
---

## Local-only fields

[공식 문서 바로 가기](https://www.apollographql.com/docs/react/local-state/managing-state-with-field-policies/)

Apollo Client에서는 Graphql 서버의 스키마에 없는 필드를 클라이언트에서만 생성 및 추가 할 수가 있다.
즉, 서버에서는 실제로 정보를 내려주지는 않지만 클라이언트에서 생성한 변수를 것처럼 query에 삽입 하는 것처럼 사용할 수가 있다.

```graphql
const GET_MOVIE = gql`
  query getMovie($movieId: String!) {
    movie(id: $movieId) {
      id
      title
      medium_cover_image
      rating
      isLiked @client # This is a local-only field
    }
  }
`;
```

위와 같은 쿼리가 있을때 isLiked 필드가 바로 Local-only fields 이다. 뒤에 @client만 붙이면 끝이다.

사용자의 다크모드 사용유무, 사용자의 timezone등을 저장할 때 사용하면 좋다고 한다.

## Local-only fields를 이용해서 좋아요 버튼 구현하기

```javascript
export default function Movie() {
  const { id } = useParams();
  const {
    data,
    loading,
    client: { cache },
  } = useQuery(GET_MOVIE, {
    variables: {
      movieId: id,
    },
  });

  if (loading) {
    return <h1>Fetching movie...</h1>;
  }

  const onClick = () => {
    cache.writeFragment({
      id: `Movie:${id}`,
      fragment: gql`
        fragment MovieFragment on Movie {
          isLiked
        }
      `,
      data: {
        isLiked: !data.movie.isLiked,
      },
    });
  };

  return (
    <Container>
      <Column>
        <Title>{loading ? 'Loading...' : `${data.movie?.title}`}</Title>
        <Subtitle>⭐️ {data?.movie?.rating}</Subtitle>
        <button onClick={onClick}>
          {data?.movie?.isLiked ? 'Unlike' : 'Like'}
        </button>
      </Column>
      <Image bg={data?.movie?.medium_cover_image} />
    </Container>
  );
}
```

css는 styled-components를 통해 작성했다.

실행하면 버튼이 하나 나오는데, 서버에서 받아온 data에 isLiked 값이 없으면 Like로 보이도록 설정했다.

그리고 Like버튼을 누르게 되면 onClick 함수가 실행된다.

onClick 함수가 실행 되면 Local-only fields인 isLiked에 기존 값의 반대값을 저장하게 된다.

onClick 함수의 중간에 생소한 패턴이 눈에 띄는데, writeFragment라는 메소드 이다.
[writeFragment 문서 바로가기](https://www.apollographql.com/docs/react/caching/cache-interaction/#writefragment)
